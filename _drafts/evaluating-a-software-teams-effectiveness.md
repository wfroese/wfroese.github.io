---
layout: post
title: "Evaluating a Software Team's Effectiveness"
excerpt_separator: <!--end_excerpt-->
tags: code teams
cover_image: /assets/images/performance.jpg
image: /assets/images/performance.jpg
cover_alt_text: a speedometer
description: Thoughts on evaluating the effectiveness of software teams
---
I used to be a software developer, and I had one job. Now I manage a software team, so I have like 87 jobs, including my old one. Now that I run a team, one of the questions I have to ask myself on a regular basis is ~~"how can I delegate 100% of my work to other people"~~, I mean, "how effective is my development team right now"? A lot has been written on this obviously, but what I need is a concise summary that I can refer to regularly to make sure we're still on track.

<!--end_excerpt-->

I would also use this as a starting point if I was considering joining a new org as a team lead or even as a developer, or for evaluating a team if I was doing some consulting. You probably wouldn't use this because you won't remember it's existence in about 30 minutes, but like, you *could*.

## What Does "Effective" Even Mean?

I think there are essentially two major questions to ask when trying to determine how effective a software team is:

1. **Efficiency:** How efficient is the team at producing software in a reliable, sustainable, secure way?
2. **Impact:** How much impact is the team's output having on the business? 

## #1. Efficiency

Evaluating a team's efficiency is a Hard Thing, but there are a lot of questions you can ask that combine to give you a good idea. Note that these questions may be answered differently depending on the environment - I'm coming from enterprise software, while e.g. embedded systems could have wildly different constraints.

1. How many bugs are users reporting? Constant firefighting is not a healthy environment, and likely means there are a number of bigger underlying issues that need addressing. 
2. How long does it take from the time a bug is reported to when a fix is in production? An acceptable time frame can vary widely by environment, but "weeks" is probably not the right answer. Unless there's no such thing as universal truth, I mean, if all truth is relative then you do you.
3. How long does it take from the time the team decides to build a feature until that feature is live in production? This is highly subjective based on the environment of course, but a little common sense can go a long way in evaluating your current state. And if you don't have a little common sense, you can always replace that with a lot of :moneybag: and a few consultants, of course.
4. How much downtime has the production system had in the last year? 
5. How often are deployments happening? Generally, the more the better - fewer, larger deployments are well known to be far more risky and cause more problems than frequent, smaller deployments.
6. How often are heroic efforts required to finish a project, fix production bugs, etc? Another indicator of sustainability - if developers are frequently required to work crazy hours, you risk burnout and increase the chances of team members leaving because they want a calmer work environment.



### Factors That Affect a Software Team's Efficiency

**Experience:** Is there enough experience on the team? The team will need experience with both software development as well as the specific domain they're working in. Does the team have a good balance of experience levels? A mix of senior, intermediate, and junior team members is often ideal. The generally accepted wisdom in my local non-tech-city seems to be "hire only people right out of school and give them no technical oversight/training/mentoring whatsoever" and, shall we say, it's not what you want.

**Specific Skills:** Does the team have sufficient skills across all the necessary tech stacks / platforms / frameworks that are in use? If your systems are built on PostgreSQL and the team hasn't managed to retain at least one member with deep PostgreSQL skills, that team is going to be in trouble.

Alternatively, you could just keep rebuilding a product over and over again with a different tech stack every time you get a new developer. I hear that worked great for Google Hangouts / Meet / Duo / WeTalk / Chat / Allo / Kero / Voice / Messages. Just kidding - two of those I completely made up, but who really knows which :thinking:

**State of the Software:** 

A system that has been well designed & maintained is much easier to change than one that hasn't.

1. How up-to-date are stacks/frameworks/libraries/servers? This is another indicator of sustainability, and whether speed of development is being temporarily achieved at the expense of large amounts of technical debt.
2. What sort of automated unit/integration test suite is in use, if any? Different environments will have different requirements, but if the automated test coverage is 0%, that's a red flag and an indicator that the software will be difficult to change without unintended side effects.
3. How many different stacks/tools are in use? This can be an indicator of major technical debt which will have a significant cost in the future if e.g. there are half-finished migrations between stacks/tools, or acquisitions have lead to many different tools in play. This mostly applies to the case where a single dev team is responsible for the variety of tools/stacks - of course, if there are multiple dev teams and each team has their own toolset, that's a different scenario that may be perfectly acceptable.

**Turnover:** How often are people leaving the team? How does the team handle losing members? Is knowledge reasonably well distributed across team members so no one person can cripple a team by leaving?



## #2. Impact

How much impact is the team really having on the business? This can be difficult because it's usually not fully under the team's control. 

Somebody has to make decisions on what exactly the team should be spending their time on. What features or new systems should they build? What manual processes should they automate? Should they instead spend time on reducing technical debt? Depending how an organization is, well, organized (my vocabulary is :100:), the development team might decide these things themselves, or they might have no input at all, or anywhere in between.

This is something management & tech leads should evaluate periodically though. Management would generally love to have their software team spend 100% of their time in New Feature Land, but will generally realize that's not sustainable. On the other hand, software teams can sometimes get lost in The Woods of Rewriting, refactoring/rewriting with the latest tech for the 9th time, and never get around to spending much time on new stuff that customers actually care about. 

What percentage of time is a development team spending on stuff that customers see? Of those projects, how many of them are determined to be useful enough to make it into production? Of the ones that make it into production, how many actually see significant use and positive feedback from customers?

### Factors That Affect a Software Team's Impact

Let's take a gander at a few key factors.

**Organizational Decision-Making:** 

1. Management's ability to decide and agree on priorities, then follow through on them by giving their teams enough time to complete projects without constantly being lead astray by the next shiny new thing. 
2. Management's decision-making process and abilities. Is the process leading to good decisions being made that result in building things customers actually want or need? If the company isn't in tune with it's customers and making a serious effort to prioritize their wants/needs, you're gonna have a bad time.

**The Balance of Power Between Tech Leads and Management:** 

If management is full of e.g. charismatic driven people, and the software team lacks sufficient experience to balance that out, the software team is likely to get railroaded into spending far too much time on features while accumulating ever more technical debt. In my experience, pretty much all software people have a tendency to over-promise, and that's especially true of less experienced folks. That leads to cutting corners and more tech debt when deadlines inevitably aren't met.

Of course, the opposite could happen as well, where the software team ends up convincing management to spend far too much time on rewrites/refactoring. Though I've heard of orgs that end up in this situation, I've never seen it - it seems far more rare than the alternative.

Note: an imbalance of power doesn't necessarily mean a team won't be effective! If the stronger side recognizes the imbalance and makes a special effort to not take advantage of it, the team can still run very well. Imagine that charismatic driven manager who knows his young tech lead doesn't have as much experience as the org would like, but takes care to encourage the tech lead to speak up and gives their input due respect and consideration. If that's the case, you have a great manager, you'll soon have a great tech lead as well, and they'll make an effective team.

**State of the Software:** 

This is a repeat, and no that's not cheating cause I make the rules around here yo.

The current state of the software affects both a team's efficiency as well as their impact though. If maintainability has been neglected for a long time and the system is a giant ball of spaghetti that everyone's afraid to touch, then the team will likely be spending a lot of time addressing technical debt. Using my super-enhanced powers of logic, I therefore deduce that the team isn't going to have much impact on the business for a while as they don't have much time to build new features, and any new features being worked on are going to take forever to finish.

## The End, In Which I Wrap This Up

And that's all folks. 

While this is hardly an exhaustive analysis (obviously, given there are books on this), I find it interesting that I always feel the need to say something like "I'm sure I've forgotten loads of stuff". If you'll allow me a slight digression (just kidding I don't care what you allow me), I feel like that phrase is a psychological crutch so that I won't feel too incompetent when someone inevitably points out stuff I didn't know or missed. So I'm not gonna say it, and when someone points out obvious stuff I didn't know I'll find another way to protect my fragile ego.

`</digression>`

Eww, who uses xml anymore. Other than like the 50% of all currently running systems that were built between 1990 and 2010, but those obviously don't count.






