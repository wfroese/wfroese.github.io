---
layout: post
title: "Software Estimation: Demystifying the Black Art"
excerpt_separator: <!--end_excerpt-->
tags: best-practices software-teams
cover_image: /assets/images/software-estimation-cover.jpg
image: /assets/images/software-estimation-cover.jpg
cover_alt_text: a shelf full of books
description: "A review - the best parts of Software Estimation: Demystifying the Black Art by Steve McConnell"
---

Classic situation: your manager comes to you and says 

> We've got a new project coming down the line - here's a spec, I need you to do an estimate - I'm thinking we can get this thing done in 8 months.

Or am I the only one whose manager tells them what they want the estimate to be before asking for an estimate?

Anyway, the "spec" is a one-page doc, and it's a bazillion dollar project that they don't want to pay a bazillion dollars for. No pressure. 

The bottom line is estimating isn't easy, and I have a hard time feeling confident in my estimates. So a few months ago when I had the chance to read through Steve McConnell's [Software Estimation: Demystifying the Black Art]( https://www.amazon.com/Software-Estimation-Demystifying-Developer-Practices/dp/0735605351/ref=sr_1_1?crid=1A2HYDAQ01MWJ&keywords=software+estimation+demystifying+the+black+art&qid=1574211099&sprefix=software+estimation%2Caps%2C179&sr=8-1 ), I picked up a lot of useful info.

<!--end_excerpt-->

Let me start with a random stat that Steve shares: **the typical organization is struggling to avoid estimates that are off by 100% or more.** They're not in a position to worry about 10-20% differences, but instead are worried about projects completely blowing up in their faces and destroying any semblance of a schedule/plan. 

When an organization is at this stage, it makes it incredibly difficult to do any serious long term planning, as you can't have any real confidence about how ongoing & upcoming software projects are going to turn out, and how much they will cost.

### Estimate vs Target vs Commitment

The first thing you need to know is exactly what the business needs, and what you're being asked for, and that's not always clear. 

**Estimate:** "a preliminary calculation of the cost of a project" - an estimate is tentative, and subject to change as new information comes to light

**Target**: Any business objective, such as "our budget is $XXX,000" , or "we need to launch this project before the Christmas holiday sales cycle". Targets are not necessarily achievable!

**Commitment**: a promise to deliver something by a specific date

The key here is to figure out what you're being asked for. When your management asks for an estimate, be sure they're not asking for a commitment, or for a plan to meet a target. Of course, I would personally never make the mistake of giving someone an estimate and having them understand it as a commitment, no sir not ever.

This communication can be tricky! I mean all communication can be tricky for me, frankly, hence the reason I got into software development in the first place. This would be the place where I reference Mr. Atwood again.

<blockquote class="twitter-tweet" data-theme="light"><p lang="en" dir="ltr">Got into computers because I enjoyed talking to machines instead of people. Now computers all about talking to people. This is some bullshit</p>&mdash; Jeff Atwood (@codinghorror) <a href="https://twitter.com/codinghorror/status/472488806126714880?ref_src=twsrc%5Etfw">May 30, 2014</a></blockquote> <script async src="https://platform.twitter.com/widgets.js" charset="utf-8"></script> 
### Random Thing About Software Projects You Want to Understand

Oh, and you probably want your management to understand this, as well.

If you draw software project outcome probabilities on a chart, you will see a hard limit to the left. That is, there is a theoretical limit for how quickly a project can be completed, and at some point, there is just no possible way it can be done in less time.

The right side of that chart, on the other hand, has a **very long tail**. There are infinite things that can and will go wrong occasionally, turning a one year project into a three year project. I totally just picked that "one year into three years" example out of thin air of course - I have no personal experience with anything like that, why do you ask.

Here, I drew a really professional visualization of this for you. That long tail on the right is [Where the Wild Things Are]( https://www.amazon.com/Where-Wild-Things-Maurice-Sendak/dp/0064431789 ), and you do not want to be there.

![Project outcome probabilities - a chart](/assets/images/project-outcome-probabilities.png)

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

1. Consider planning for X% increase in requirements. NASA plans for 40% (!!!!! You're not crazy after all Will, this is normal, literally nobody can figure out what the hell they want to build before they build it...)
2. Never give estimates off the top of your head. The answer is always always always "I'll look into it and get back to you."
3. As the project team gets bigger, the number of communication paths goes up, causing productivity to go down. Factor team size into the estimate.
4. Management effort often amounts to 10-12% of total effort, for projects < 100K LOC
5. Technical effort is often divided up as: 15% architecture, 60% construction, 25% QA

### An Estimating Workflow

The book covers several different estimation methods, but I'll cover two here.

**Count & Compute**

1. **Count** things. You could count features, bugs, user stories, web pages, reports, database tables, etc. The key is to count something that is closely correlated with the size of the software you're building. Steve says that statistically, you need a count of at least 20 for the count to be meaningful.
2. **Compute** things. Here's where you pull out the perfectly curated historical estimate data that you've been tracking for a while. If you counted out 18 different reports that need building, and you know that the past 10 reports you built averaged out to 30 hours, then your estimate is simply 18 * 30 = 540 hours.

Apparently this simple averaging of historical data is proven to be quite accurate (proven by like, research and stuff), which surprised me a little. Of course, we didn't have any historical data on our team - I've since seen the light and realized how valuable it can be, so I've started tracking some of it.

**Individual Expert Judgement**

1. Take the large project and divide it into smaller tasks, where each task is no more than two days of effort.
2. Do **best and worst case estimates** for each of the tasks. In many cases, the worst case estimate will be far, far higher than the best case estimate.
3. Estimate a "most likely case" for each task, simply using judgement. This is likely to be closer to the best case than the worst case, for most tasks.
4. Calculate the "expected case" with the following formula: 

> Expected Case = [BestCase + (4 x MostLikelyCase) + WorstCase] / 6

This formula accounts for the full width of the best-to-worst case range, and also factors in the most likely case. 

### Activities Commonly Forgotten in Estimates

My estimates are always perfect, but I'm sure *you* forget to include things all the time. Steve's got a list of about 40 things, but here are the ones most relevant for myself:

1. Ramp-up time for new hires
2. Learning new development tools/frameworks/languages
3. Writing documentation: technical, user guides, etc
4. Support of existing systems during the project, which means you'll have less time on the new project, thereby extending any commitments
5. Performance tuning
6. Doing demos to management, customers, end-users etc
7. Setting up build/deploy pipelines
8. Time spent clarifying and refining requirements - even if you thought they were clear before you started writing code, you inevitably find out they weren't clear enough

### Estimate Adjustment Factors

The book lists a set of factors that affect project outcomes and defines how much each factor can affect a project in a best and worst case scenario. This chart can be used to adjust an estimate based on each factor in your specific context.

For example, the first item is "Product Complexity", which can decrease total effort by as much as 27% for low-complexity projects and increase total effort by as much as 74% for high-complexity projects. Of course, your project is likely somewhere in between - you define that, and apply the adjustment as appropriate.

|Factor|Best Case|Worst Case|
| -------------------------------- | ---- | ---- |
| Product Complexity               | -27% | +74% |
| Requirements Analyst Capability  | -29% | +42% |
| Programmer Capability            | -24% | +34% |
| Personnel Continuity (Turnover)  | -19% | +29% |
| Required Software Reliability    | -18% | +26% |
| Extent of Required Documentation | -19% | +23% |
| Domain Experience                | -19% | +22% |
| Language & Tools Experience      | -16% | +20% |
| Database Size                    | -10% | +28% |
| Developed for Reuse              | -5%  | +24% |
| Team Cohesion                    | -14% | +11% |

### End

I'd like to say that estimation is now nice and easy for me, all thanks to this book.. so I will!

Estimation is now nice and easy for me, all thanks to this book. 

In other news, don't believe everything you read on the internet, folks. In reality though, here's how this book (mildly) changed my life:

1. I have a touch less of the ol' imposter syndrome when estimating big projects. I've filled in a few gaps in my estimating methodology, and now feel comfortable that I'm not missing anything major.
2. I started tracking some historical estimate vs outcome data, in hopes that it will be useful once there are enough data points.
3. I just wrote this here fancy reference post, which I will come back to when I next have to estimate a bazillion dollar project from a one-page "spec". I'll use the "Activities Commonly Forgotten", and "Adjustment Factors" to improve my estimate as needed.













