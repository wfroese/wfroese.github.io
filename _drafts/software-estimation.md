---
layout: post
title: "Software Estimation: Demystifying the Black Art"
excerpt_separator: <!--end_excerpt-->
tags: best-practices software-teams
cover_image: /assets/images/pr-review.jpg
image: /assets/images/pr-review.jpg
cover_alt_text: a screen showing some code
description: My favorite parts of Software Estimation: Demystifying the Black Art by Steve McConnell

---

A few months ago I had the chance to read through Steve McConnell's [Software Estimation: Demystifying the Black Art]( https://www.amazon.com/Software-Estimation-Demystifying-Developer-Practices/dp/0735605351/ref=sr_1_1?crid=1A2HYDAQ01MWJ&keywords=software+estimation+demystifying+the+black+art&qid=1574211099&sprefix=software+estimation%2Caps%2C179&sr=8-1 ). Until this book I had about as much confidence in my estimates as TODO

The book isn't overly long, at 275 pages, which is fantastic compared to Steve's [Code Complete]( https://www.amazon.com/Code-Complete-Practical-Handbook-Construction/dp/0735619670/ref=sr_1_1?keywords=code+complete&qid=1574211216&sr=8-1 ), which is a monstrosity (albeit a very good one!) checking in at 960 pages. 

Anyway, this book was so incredibly useful I simply had to take a lot of notes, and I've reviewed those notes several times since, trying to remember everything. 

<!--end_excerpt-->

Let me start with a random stat that Steve shares: **the typical organization is struggling to avoid estimates that are off by 100% or more.** They're not in a position to worry about 10-20% differences, but instead are worried about projects completely blowing up in their faces and destroying any semblance of a schedule/plan. When an organization is at this stage, it makes it incredibly difficult to do any serious long term planning, as you can't have any real confidence about how ongoing & upcoming software projects are going to turn out, and how much they will cost.

Now, I'm sure this number varies by industry and size of the company. In my experience it checks out though, especially with larger projects.

### Estimate vs Target vs Commitment

It turns out the first thing you need to know exactly what the business needs, and what you're being asked for, and that's not always clear. 

**Estimate:** "a preliminary calculation of the cost of a project" - an estimate is tentative, and subject to change as new information comes to light

**Target**: Any business objective, such as "our budget is $XXX,000" , or "we need to launch this project before the Christmas holiday sales cycle". Targets are not necessarily achievable!

**Commitment**: a promise to deliver something by a specific date

The key here is to figure out what you're being asked for. When your management asks for an estimate, be sure they're not asking for a commitment, or for a plan to meet a target. Of course, I would personally never make the mistake of giving someone an estimate and having them understand it as a commitment, no sir not ever.

This communication can be tricky! I mean all communication can be tricky for me, frankly, hence the reason I got into software development in the first place. This would be the place where I quote Mr. Atwood again.

> *Got into computers because I enjoyed talking to machines instead of people. Now computers are all about talking to people. This is some bullshit* 
>
> -- Jeff Atwood

### Random Thing About Software Projects You Want to Understand

Oh, and you probably want your management to understand this, as well.

If you draw software project outcomes on a chart, you will see a hard limit to the left. That is, there is a theoretical limit for how quickly a project can be completed, and at some point, there is just no possible way it can be done in less time.

The right side of that chart, on the other hand, has a **very long tail**. There are infinite things that can and will go wrong occasionally, turning a one year project into a three year project. I totally just picked that "one year into three years" example out of thin air, I have no personal experience with anything like that, why do you ask.

### What is a "Good" Estimate?

Steve's definition of a "good" estimate is as follows:

> A good estimation approach should provide estimates that are within 25% of the actual results 75% of the time

You know when I first read that, I kinda thought that was a pretty low standard. And who doesn't like low standards!

And then I thought about it some more, and let me tell you, estimating 6-12 month projects to that level of accuracy is pretty unbelievably hard.

Steve follows up with a more general definition of a "good" estimate:

> A good estimate is an estimate that provides a clear enough view of the project reality to allow the project leadership to make good decisions about how to control the project to hit its targets.

And here I thought this whole time that a good estimate was one that confirmed what my manager wanted to hear. Who knew?

### Psychological Thing for Me to Remember

> If you are feeling pressure to make your ranges narrower, verify that the pressure actually is coming from an external source and not from yourself.

Man, I have never felt so attacked in my life. I'm a people-pleaser Steve, I can't help it - stop yelling at me.

### Several Factors to Consider When Estimating

1. Consider planning for X% increase in requirements. NASA plans for 40% (!!!!! You're not crazy after all Will, this is normal, everybody is doing it...)
2. Never give estimates off the top of your head. The answer is always always always "I'll look into it and get back to you."
3. As the project team gets bigger, the number of communication paths goes up, causing productivity to go down. Factor team size into the estimate.
4. Management effort often amounts to 10-12% of total effort, for projects < 100K LOC
5. Technical effort is often divided up as: 15% architecture, 60% construction, 25% QA



### An Estimating Workflow

The book covers a several different estimation methods, but I'll cover two here.

**Count & Compute**

1. **Count** things. You could count features, bugs, user stories, web pages, reports, database tables, etc. The key is to count something that is closely correlated with the size of the software you're building. Steve says that statistically, you need a count of at least 20 for the count to be meaningful.
2. **Compute** things. Here's where you pull out the perfectly curated historical estimate data that you've been tracking for a while. If you counted out 18 different reports that need building, and you know that the past 10 reports you built averaged out to 30 hours, then your estimate is simply 18 * 30 = 540 hours.

Apparently this simple averaging of historical data is proven to be quite accurate, which surprised me a little. Of course, we didn't have any historical data - I've since seen the light and realized how valuable it can be, so I've started tracking some of it.

**Individual Expert Judgement**

1. Take the large project and divide it into smaller tasks, where each task is no more than two days of effort.
2. Do **best and worst case estimates** for each of the tasks. In many cases, the worst case estimate will be far, far higher than the best case estimate.
3. Estimate a "most likely case" for each task, simply using judgement. This is likely to be closer to the best case than the worst case, for most tasks.
4. Calculate the "expected case" with the following formula: 

> Expected Case = [BestCase + (4 x MostLikelyCase) + WorstCase] / 6

This formula accounts for the full with of the best-to-worst case range, and also factors in the most likely case. 

### Activities Commonly Forgotten in Estimates



### Estimate Adjustment Factors







