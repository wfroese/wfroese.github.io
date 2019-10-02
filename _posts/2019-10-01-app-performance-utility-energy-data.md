---
draft: true
layout: post
title: "Performance: A Production Story (or, how to use 350 GBs of RAM)"
excerpt_separator: <!--end_excerpt-->
tags: code performance energy-data
cover_image: /assets/images/performance.jpg
cover_alt_text: a speedometer
description: Thoughts on application performance when working with utility energy data
---
One thing I find interesting about working in the utility industry is that you always have to be watching out for performance issues because of the large amounts of data.

<!--end_excerpt-->

I've always liked performance tuning because of how satisfying it is when I can get an app running quicker with changes that are often seemingly minor. I've had two particularly fun cases over the last few years that illustrate why performance is so important when dealing with energy data.

## Iterating Over Large Collections
In the first case, we found that a certain loading process was incredibly slow for a new customer that had around twice as many meters as the previous largest customer. Now, in general you would assume that a process would likely take twice as long for twice as many meters, but we were seeing run times of hours when we expected minutes.

After doing some digging, I uncovered a bit of code written long ago that essentially boiled down to the block below:

{% highlight csharp %}

// 1. Set up, for performance testing purposes - define the number of meters and readings, and generate a list of reading objects
int numMeters = 50000;
int numReadings = 1000000;
List<Reading> readings = new List<Reading>();
Random randomGenerator = new Random(DateTime.Now.Second);
for (int i = 0; i < numReadings; i++)
{
    readings.Add(new Reading { SerialNumber = randomGenerator.Next(numMeters).ToString() });
}

// 2. Run through the readings and create a meter object for each unique serial number we find
List<Meter> meters = new List<Meter>();
foreach (Reading reading in readings)
{
    Meter meter = meters.SingleOrDefault(x => x.SerialNumber.Equals(reading.SerialNumber));
    if (meter == null)
    {
        meter = new Meter { SerialNumber = reading.SerialNumber };
        meters.Add(meter);
    }
}

{% endhighlight %}

And the performance of the `foreach` block that loops through the readings was not good, especially given that it was running through a million plus readings for > 100,000 meters.

And so after taking a closer look, I realized the problem was that `.SingleOrDefault` was going through the list of meters one-by-one to find the object with the correct serial number, and the complexity of this is O(m*n), where m = the number of meters and n = the number of readings.

O(m*n) is often generalized to O(n^2), meaning this algorithm had an exponential run-time, which explained why it got so much worse when we only doubled the amount of meters.

### The Solution
Improving on this code was fairly trivial, so I took two possible solutions and tested their performance to compare.

{% highlight csharp %}

// 3. Method Two: Run through the readings and create a meter object for each unique serial number we find,
// but this time keep the meters in a Dictionary instead of a List.
Dictionary<string, Meter> meters2 = new Dictionary<string, Meter>();
foreach (Reading reading in readings)
{
    if (!meters2.ContainsKey(reading.SerialNumber))
    {
        Meter meter = new Meter { SerialNumber = reading.SerialNumber };
        meters2.Add(reading.SerialNumber, meter);
    }
}

// 4. Method Three: Pure LINQ
List<Meter> meters3 = 
    readings
    .GroupBy(x => x.SerialNumber)
    .Select(x => new Meter { SerialNumber = x.Key })
    .ToList();

{% endhighlight %}

### Results

||Method One|Method Two|Method Three|
|---+---+---+---|
|10,000 meters, 10,000 readings|1.3s|15 ms|5 ms|
|10,000 meters, 100,000 readings|34s|30 ms|28 ms|
|20,000 meters, 100,000 readings|67s|21 ms|30 ms|
|10,000 meters, 200,000 readings|69s|23 ms|40 ms|
|20,000 meters, 200,000 readings|148s|29 ms|160 ms|
|50,000 meters, 1,000,000 readings|26 minutes|150 ms|700 ms|
|100,000 meters, 2,000,000 readings|Probably infinity, who can say|407 ms|1.2s|

With method 1, this task becomes literally impossible pretty quickly as the number of meters and readings grows, while with methods 2 & 3 this is a nearly trivial task.

## You Want *How Much* RAM??
My second fun story comes again from a data loading process. We were doing some stress testing to see how many meters & readings our system could feasibly load into the database in realistic times when we started to see the RAM usage of the loading process spike.

After some investigation, we found the loading process had the following:

{% highlight csharp %}

XmlDocument doc = new XmlDocument();
doc.Load(file);
XmlNodeList meterReadingNodes = doc.GetElementsByTagName("MeterReadings");

{% endhighlight %}

This code looks perfectly fine, but it turns out it's the naive implementation and the `XmlDocument` class isn't intended to be used for large xml files, because it actually loads an in-memory representation of the entire file into memory. And unfortunately, that in-memory representation of the file is many times larger than the actual file itself.

In our simulation we were loading data for 2 million meters from one xml file. I don't remember the exact size of the file, but my best guess is in the neighborhood of 1GB.

We found that our app required **343GB of RAM** to load that file into memory. 

In the end, the solution was just to stop using `XmlDocument` and use `XmlReader` instead:

{% highlight csharp %}

public static IEnumerable<XmlElement> MeterReadings(this XmlReader source)
{
    while (source.Read())
    {
        if (source.NodeType == XmlNodeType.Element && source.Name == "MeterReadings")
        {
            XmlDocument doc = new XmlDocument();

            doc.LoadXml(source.ReadOuterXml());
            yield return doc.DocumentElement;
        }
    }
}

using (XmlReader reader = XmlReader.Create(_File))
{
    IEnumerable<XmlElement> meterReadings = from xe in reader.MeterReadings() select xe;

    // ...
}

{% endhighlight %}

We ended up finding that `XmlReader` performance was basically identical to `XmlDocument`, without the need for several hundred GBs of RAM.

## Conclusion


