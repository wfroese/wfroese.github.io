---
layout: post
title: "Software Development in the Utility Industry"
excerpt_separator: <!--end_excerpt-->
tags: utility-industry energy-data
cover_image: /assets/images/earth-electricity.jpg
image: /assets/images/earth-electricity.jpg
cover_alt_text: the earth from space, showing lights from cities
description: What software development is like in the electrical utility industry
---

All companies are software companies in 2019, but there's a fairly large variance in how fast companies adopt the latest software advancements, particularly along industry lines. In some industries you move fast and break things, and other industries you wait two weeks for people to respond to emails so you can do some actual work. 

This makes the software landscape quite a bit different in some industries than others. Regulated industries like healthcare, for example, are obviously slower than unregulated industries and that leads to all kinds of differences in how a software team in healthcare operates compared to a team working on a startup in marketing.

I'm always interested in hearing from other developers what it's like working in their domain so I thought it might be interesting to review the state of software in the (electric/water) utility industry, from a software developer's perspective. 

<!--end_excerpt-->

## Context

A quick bit of context: [Utilismart]( http://www.utilismartcorp.com/ ) is a meter data management company, and we at [Eleven Winds]( https://www.elevenwinds.com/ ) are their software development team. I've been working with Utilismart for about four years now and I'm finally starting to get a feel for what the broader industry is like, though I'm not an expert by a long shot.

![Wind turbines on the horizon](/assets/images/windmills.jpg)

## The Industry

If you want to understand what software development in the utility industry is like, first you have to understand a few things about the industry in general. Because what's more thrilling than talking about the details of basic infastructure that we all take for granted?

#### **Utilities are mostly small companies**

In the grand scheme of things, electric and water utility companies are mostly small. Imagine how many small towns and cities there are across central Canada and the US, and then realize that many of them have their own utility.

Most utilities are small enough that it's entirely unrealistic for them to have their own software team. This means there's a large (and increasing) demand for software tools & platforms for utilities as they look to modernize their operations. And since that demand isn't being filled by the utilities themselves, third-party software vendors have stepped in to offer a variety of SaaS and on-premises solutions.

Social media is an example where the companies themselves are the ones pushing the limits and innovating. In the utility industry, that's just not the case.

### Utilities are sticky customers

Migrating a utility company onto a new software platform isn't simple, easy, or quick for anyone involved. So when a utility buys software from a third-party, they are likely to be staying on that platform for a long time.

This means that third-party vendors put a lot of energy into sales. The lifetime value of customers is very high, and the majority of the work is done upfront with the initial onboarding.

Retaining customers is fairly easy though, relative to the initial onboarding, and you can generally expect to retain customers for many years.

### There are a huge number of third-party vendors

There are many relatively small vendors in the industry, resulting in a lot of fragmentation. There are very few end-to-end providers, meaning that utilities are piecing together solutions with multiple vendors.

![Power lines under dark sky](/assets/images/powerlines.jpg)
### Modern Utilities Need a Lot of Software

There are a lot of moving parts to a modern utility, and each one needs software to run. Some of these different areas are:

1. A Customer Information System (CIS), which stores residential customers, addresses, account numbers, etc.
2. Advanced Metering Infrastructure (AMI), which communicates directly with smart meters to retrieve readings and usually outputs daily XML or CSV files containing meter readings
3. Meter Data Management - store all the generated meter readings, estimate readings that couldn't be retrieved, export data to billing systems
4. GIS - storing geographical data for meters, generating network models, etc
5. Work Management - planning maintenance and installation of new lines, transformers, meters, etc., tracking inventory (meters, poles, transformers, etc)
6. Outage detection and management
7. Finance & Accounting

There's a lot of overlap between these areas and the data that is needed for each one, but it's normal for a utility to meet these needs with 3-5 different tools/vendors.

### Relying on multiple third-party tools requires a lot of integration work

Utilities have 99 problems, and one of them is always integrations between all the different software they're using. It's rare for them to be able to buy a single platform that meets all their needs, and a significant amount of data needs to be shared across all the systems they use. This means the third-party tools they buy have to integrate, and the onboarding process often involves some custom development to make that integration happen.

In the US there has been some success addressing this problem with [Multispeak]( https://www.multispeak.org/what-is-multispeak/ ), a collaboratively defined web service specification for making systems interoperable in the utility industry. Support for Multispeak among the third-party vendor tools is not consistent though, and even among the ones that do support it there are now several different versions. Most vendors only support one of the versions, so if you're doing integrations between several tools, you might end up using a different Multispeak version for each one.

### The industry is shifting towards operating in real-time

Utilities increasingly need to be able to respond to events in real time. Demand/Response programs are being developed where utilities need to be able to respond to grid peaks by incentivizing customers to reduce their power usage temporarily, and this needs to happen in real-time. This means needing to ingest data in real time (rather than once a day), and also responding to these events at any time, as needed.

![A laptop displaying a web application](/assets/images/laptop-with-app.jpg)

## The Software

I talked a bit about what utility companies use software for exactly, but I want to also look at what sort of programming languages, platforms, & development tools are used. There's inevitably a lot more going on in the industry than I've been exposed to, but here's what I've seen.

### Big Data

A single meter producing a reading at intervals of 15 minutes will produce 35,000 readings a year. If you're a vendor providing services to many utilities, you might have a million (or 50 million!) meters in your system generating a few billion readings per year. This is one of the biggest problems in the utility space as the amount of data keeps on growing, and they just can't find enough floppy disks to store them all on. 

I'm kidding - they've moved past floppy disks, like two years ago, at least.

Oracle and SQL Server seems to be fairly common database systems, but there is also beginning to be a movement away from traditional relational databases towards specialized time-series databases. One such example is [Kx for sensors]( https://kx.com/solutions/utilities/ ).

### Web Services

In my experience, there is not a RESTful API or any JSON to be seen. XML and SOAP continue to be the standard, especially because the Multispeak protocol commonly used in the industry is based on SOAP.

### The Cloud + Infrastructure as Code

There's been a trend the last several years towards building infrastructure as code, which has gone hand-in-hand with the public cloud companies building out their infrastructure in programmable ways. 

The utility industry has been slow to adapt to these though, which isn't surprising - it's been slow to adapt to most software trends. In my experience, most software in this space is on premises or in private data centers, though that may be because most of my experience is with smaller companies.

### Machine Learning and AI

If statements are pretty popular these days, folks. Machine learning and AI are interesting, because a lot of the major vendors love to put them in their marketing materials. As usual, it's a bit difficult to pick out who's just throwing them up because they're nice buzz words, and who's actually using the tech.

From what I've seen, machine learning and AI are in the very, very early stages of being adopted in the industry. At this point, there are a number of pilot & research projects going on to investigate what the possibilities are, but I haven't been able to find much concrete evidence of usage in actual production environments.

There are potential use cases though, such as improving forecasting of how much energy a windmill will generate over the next few days, predicting power outages, etc.

## Improving energy systems has a practical, positive impact on society

If you like to feel that your work is practical, useful, has a positive impact on society, and bores most people to tears, this might be the industry for you. Not everybody cares what industry they work in, but for myself, it helps to get me through the hard days knowing that I'm not working on selling more ads to more people.  





