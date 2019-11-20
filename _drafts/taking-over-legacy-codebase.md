---
layout: post
title: "Taking Over a Legacy Codebase"
excerpt_separator: <!--end_excerpt-->
tags: code best-practices software-teams
cover_image: /assets/images/pr-review.jpg
image: /assets/images/pr-review.jpg
cover_alt_text: a screen showing some code
description: How to modernize a legacy codebase
---

Earlier this year I was put in charge of the team that was taking over all software development for a client of ours. 

Unfortunately, the code base was not in a good state (that's what we in the business call an understatement), and that was causing a lot of problems for the client. I had been working in parts of this code base for a few years, but now that I was running the entire team, I finally had the chance to address the root of the problem, rather than just putting in patches on top of patches.

<!--end_excerpt-->

>  “To me, legacy code is simply code without tests.” 
>
> -- Michael C.  Feathers, [Working Effectively with Legacy Code](https://www.goodreads.com/work/quotes/44241) 

This is a fairly well-known quote describing what might be considered "legacy" code, from a book that I should probably even read one of these days. Unfortunately there are a lot more things that can go wrong with a code base than just not having tests, though.

The code base we were taking over had a lot of issues:

1. Bugs being reported regularly
2. No tests of any kind
3. Very little documentation
4. Many disparate frameworks and languages being used
5. Severely outdated frameworks and platforms in some places

Now, as a developer, I would love to have as much time as I needed to fix all these issues. As it turns out though, this was like, a real business, and they tell me real businesses have existing clients with real needs and stuff, who knew.

So I was left trying to strike a balance between meeting immediate needs and addressing some of the bigger issues that were slowing down development. This is the story of how we approached the situation.

## #1. Educate Management

Step one was to make management aware of the situation. This is a delicate topic, because you don't want to come across as claiming everyone at the company involved with the software has done a terrible job, or that all your predecessors were terrible developers (even if that's true!). 

That wasn't really the case here anyway - in this situation, I think the issues were more structural, rather than the responsibility of any one person. Basically, there had been a lot of turnover for several years, and several third-party development teams, so nobody had been around long enough to enforce any cohesion between the different systems & teams. This basically lead to complete chaos throughout the code base, and let me tell you, I was just **shocked** to find out this lead to even more turnover, when developers realized they didn't want to deal with the mess.

One thing I regularly find is that non-technical management doesn't understand how these sorts of issues actually affect their business. I think this is because the impact is not easily measurable, and the effects often aren't seen in the short term.

Here's a few examples of what I mean:

### Lack of Tests

When developers are always rushed, tests are one of the first things that get dropped. Lack of automated unit/integration tests, especially around the really tricky core business logic, makes it much more difficult (read: more expensive) to safely make changes a few years down the road when the original developer is long gone.

And let's be real - I pretty much have to bribe people to get them to write unit tests. Writing tests is **boring as heck** for a lot of developers, and yet they are **absolutely critical** especially for core business logic, so if you ever want to write software that other developers don't hate working on, **suck it up and write the tests**. I'll stop bolding stuff now.

### Lack of Documentation

Without documentation, there's no way for developers to get up to speed on the domain, the various systems in play, how they interact, etc. This means bringing new developers onboard is a lot slower and more expensive than necessary, and often results in a lot more mistakes/bugs from new developers because they don't understand the system as well as they need to.

On the plus side, writing large complicated systems with no documentation equals job security, amirite?

### Too Many Frameworks/Platforms/Tools

More languages/platforms/tools make development inherently more complex. If you expect a small team to work in Java, .NET, PHP, React, and Silverlight, those developers are never going to build up expertise in any of those platforms/frameworks. This, again, makes development slower (read: more expensive).

### Outdated Tech

Sometimes it can make business sense to keep software running on outdated platforms & frameworks, rather than taking on expensive rewrites. 

But one factor that needs to be considered is that developers only have so much tolerance for dealing with outdated stuff - if too much of their job becomes dealing with that old Silverlight app, they will leave. And, in case you haven't gotten the theme here yet, developer turnover is costly - it's ridiculously expensive to find, interview, and train new developers.

Sidenote: Silverlight, in 2019. It boggles the mind.

## #2. Fix Critical Bugs

This actually goes hand-in-hand with #1. Critical bugs need to be fixed first, obviously, to avoid losing customers. 

These bug fixes in the early stages are not likely to be pretty, and you can't write any tests for them - none of the code is designed to be testable, and you can't exactly do major refactoring at this point to get there.

## #3. Documentation

When you're starting from scratch on a new system, you'll spend a lot of time figuring out the basics. This is the best time to start writing documentation because you're in the middle of the struggles yourself, so you know exactly what someone in that position needs.

Some examples of basic, critical documentation that every project needs:

1. Developer environment setup - the frameworks and tools that need to be installed, the configuration that needs to be set up, where the code is checked out from, where the dev & QA databases are (or how to set one up), etc. 
2. A high-level overview of the domain - define terminology, major customer use cases, etc.
3. A high-level overview of the system, especially if there are many different parts involved. This would be e.g. a listing (along with brief descriptions) of all the services, web apps, components, etc.
4. Deployments - if you don't yet have automated deployments, you need detailed docs explaining how deployments are done of every single application in the system.
5. Customer onboarding - in industries/environments where onboarding a new customer is a non-trivial task, you absolutely need an in-depth guide listing all the steps involved and explaining how to do each one

If you're anything like us, you'll also struggle to convince people to put enough energy into writing decent documentation. It's like, we're sitting here cursing our predecessors for not writing any documentation, **while not caring enough to write any documentation ourselves**. The irony, man.

## #4. Automated Deployments & Rollbacks

For us, the next most critical improvement was to build automated deployments & rollbacks for every sub-system. Automating these processes obviously means you can do them consistently error-free and reduces stress on the people doing the deployments, and these are really positive things, but they are really just a means to an end.

**The end goal here is that you want to be deploying as often as possible**, and to get there, you need to remove as much friction from the process as possible. 

Big bang deployments after weeks or months of work are incredibly risky, **especially** when you have a system without automated tests. In that situation, you simply can't manually test every single thing that needs re-testing when a major change is happening. There are too many things to test, and some cases are going to be missed, resulting in bugs and frustrated customers.

In contrast, small deployments done often are inherently less risky because they're easier to test, since their impact on the system is going to be smaller.

### More Management Education

It depends on the situation, but for us, this step required a lot more work educating the management team. They were so used to deployments going wrong (because deployments were manual, and included too much stuff), that they became extremely risk averse, which lead to deployments being done even less often and including even more stuff, etc.

Breaking out of this cycle wasn't particularly easy and took a lot of patience, as organizational change often does.

I'm going to quote Jeff Atwood again, because this is basically my life's motto, and I'm trying to set a world record for how many times you can use the same quote in context:

>  *Got into computers because I enjoyed talking to machines instead of people. Now computers are all about talking to people. This is some bullshit* 
>
> -- Jeff Atwood

## #5. Make a Plan to Address Technical Debt

So at this point, management is aware of the situation, there are no outstanding critical bugs, you've got a decent start on critical documentation, and you're put yourself in position to deploy smoothly and frequently.

This is where things really start to get tricky because you've taken care of most of the low-hanging fruit, and yet there's still so much technical debt in the code base making it very difficult to make any progress.

[The Developer Coefficient]( https://stripe.com/reports/developer-coefficient-2018 ), a report from Stripe, indicates that developers spend ~40% of their time on maintenance, on average.

**Sidenote**: Stripe just has incredible designs for every single thing they put out. That website is gorgeous, the PDF is gorgeous, everything is gorgeous. 

![Chart showing developers spend 40% of time on maintenance](/assets/images/developer-coefficient-maintenance.jpg)

Now, this tells me that if you have a code base that has significantly more technical debt that average (though it's debatable what an average amount of technical debt is), then your team will need more than 40% of their time spent on technical debt in order to make any progress.

### Even More Management Education

This, needless to say, needs to be made clear to management. The specific numbers (e.g. 40%) might be arguable, and might differ somewhat in depending on the specific environment, but the key is that significant amounts of time need to be made available to deal with technical debt, or you'll never be able to speed up the development team as a whole.

If you simply can't get management to buy in to this fact, then your development team is going to continue to struggle slowly along, putting patches on top of more patches, making life ever more miserable for everyone working on the system. That's a good time to consider a mid-life crisis sabbatical, or, you know, other career options.

If, on the other hand, management understands the situation then you can make a plan that allows for significant time to address technical debt while also allowing some time for new development.

In our case, we had two major issues remaining to address in our plan.

### Automated Tests

None of our applications were designed to be unit tested, so we started with some integration tests. This was a "anything is better than nothing" approach, and allowed us to make sure we weren't accidentally breaking any major features that were unexpectedly coupled to new code we were writing. 

For unit tests, we took several approaches:

1. Immediately agreed that all new sub-systems would be designed to include tests, and would include tests from the start. 
2. When we had a sub-system that needed significant changes for a new feature, we took that opportunity to do significant refactoring and adding tests, since the new feature was going to require significant manual testing anyway.
3. Ok fine, we have only two approaches - I really need to read [Working Effectively with Legacy Code]( https://www.amazon.com/Working-Effectively-Legacy-Michael-Feathers/dp/0131177052/ref=sr_1_1?keywords=working+effectively+with+legacy+code&qid=1574043203&sr=8-1 ), because that's all I've got at this point. Legacy code sucks y'all.

This is pretty much where our team is at right now. We've made some progress on this step, but there's so much more work to do.

### Too Many Tools

This is the other major issue our team is struggling with right now. We're a team of five, and I only write code 25% of the time, so 4.25 developers. And yet, we have to be able to build things using:

1. C#: Windows services, ASP.NET, ASP.NET Core, 
2. PHP (with Laravel), and "old school" javascript with jQuery (jQuery is like more than two years old - gross)
3. Silverlight (which we actually just got rid of! I can die in peace now)
4. Java
5. React
6. Oracle and PL/SQL, which is a programming language itself
7. Kx for Sensors - a third-party time-series database specialized for handling sensor data
8. A network automation tool called Automate, which has it's own programming language
9. Windows & Linux servers

Look at that, I almost made myself cry just typing out that list. 

Anyway, my point is, that is **way too much for a small team**, and you should never, ever, under any circumstances, let your team introduce that many tools into one system or code base.

It is acceptable to have two different platforms/languages, especially if you're in the process of migrating. It might even be acceptable to have five different languages/platforms if you have five different independent teams. But this many platforms/languages for one team is just sheer neglect.

/endrant

## End

Anyway, that's about it. This is the part where y'all can tell me all about the obvious things I'm missing and what I'm doing wrong. Please do so on twitter [@willfroese]( https://twitter.com/willfroese _)!

**Bonus: ** I was gonna write about the Strangler Pattern (like [this]( https://martinfowler.com/bliki/StranglerFigApplication.html ) and [this]( https://docs.microsoft.com/en-us/azure/architecture/patterns/strangler )), but then didn't. It's a cool pattern (you can tell by how dangerous it sounds) - you should check it out!