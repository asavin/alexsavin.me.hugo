+++ 
draft = false 
date = 2024-01-18T01:37:10Z
title = "Post Office, Horizon - and large scale software projects"
description = "Learnings from Post Office Horizon debacle"
slug = "2024-01-18-post-office-horizon-learnings" 
tags = ['software', 'delivery', 'SRE']
categories = []
externalLink = ""
series = []
+++

They say when interviewing for a job at NASA you are asked to name as many mistakes as you can from a 1998 movie Armageddon. In the UK we could probably do the same, but with the [Post Office scandal](https://en.wikipedia.org/wiki/British_Post_Office_scandal#Horizon_IT_system) and the nationwide rollout of the Horizon IT system.

And yes, Mr Bates vs the Post Office is a brilliant show, go see it.

So, given the wiki article, the show, and the 300 pages long [High Court ruling](https://www.judiciary.uk/wp-content/uploads/2019/12/bates-v-post-office-judgment.pdf) let me do just that.

## User impersonation

Logging in as another user can be a feature of an authentication provider. Auth0 used to have it by default, but in 2022 chose to deprecate it - and that actually should tell you a lot. I used to work on a large scale project where we'd routinely employ this feature of Auth0 when debugging user issues - as I'm sure many others.

The difference though is this should only happen with user's permission - and only on systems where no user sensitive data is stored. Today I'd argue that such systems do not exist, and any product with user auth will contain user sensitive data that could be exploited by a bad actor. Which is why Auth0 has deprecated user impersonation - and why you shouldn't be doing this at all.

There are a number of better approaches that would not expose user data, and would allow to debug user journey issues:

* Distributed tracing of user journey on backend - for example, with Open Telemetry
* Data integrity checks on your database level
* Client-side telemetry - but omitting PII

## Testing in production

You always have staging environment, and sometimes it is separate from production.

Having a test environment is not difficult, and I'm sure Horizon had one. The problem is data. With massive large scale projects your production data is vastly different from the test env data. And with real world data come real world bugs.

One of the solutions that have definitely happened is to copy data from prod to test env. It will be immediately outdated, but it still will be better than whatever test data there was. Might even allow for a more reliable testing, and will help to uncover some of the software issues.

Please don't do that.

Testing new functionality in production is a legitimate option, and I wrote a [whole thing](https://alexsavin.me/posts/2023-01-17-tests-in-production/) about just that. There are rules though:

* Use feature flags
* Use shadow mode
* Provide users with an option to enroll into this "beta feature"
* Collect telemetry

## User experience

Horizon was originally procured in 1994, and started rollout 6 good years later in 2000. The main issue seems to be discrepancies in the transactions.

*"The system had, according to the report, not been tracking money from lottery terminals, Vehicle Excise Duty payments or cash machine transactions – and the initial Post Office Ltd investigation had not looked for the cause of the errors, instead accusing the subpostmasters of theft"*
[source](https://www.bbc.co.uk/news/uk-29130897)

A fair assumption here is that the developers of the system have largely failed on the UX research and likely developed the system in vacuum. Probably not. I bet there was a UX research of some kind at the beginning of the project - and a lot of firefighting later on.

A better approach would be a continuus UX research across the UK, visiting as many Post Office locations as possible, running interviews, observing work, and collecting as much user behaviour data as possible. This would highlight various types of customer interactions that are directly related to the Horizon system requirements. This research should be run annually since things do change all the time, new store features are introduced, and people do change their behaviour too.

At this point you might be asking on the cost of such a large scale UX project - and I can guarantee you it will be cheaper than the cost of shipping a badly designed product designed to be used by almost 100% of UK population. Actually, let's do some napkin math:

```
11500 Post Office branches total
UX research of 100 different branches every year
2x UX researchers visiting 10 branches / year
20 UX researchers contracted at £500 / day
1 work week per branch of research and observation
5 days * 20 researchers * 10 branches = 1000 days
1 work week per branch to document the observations = 2000 days
2000 days * £500 = £1000000.00
```

One million pounds is not a small penny, but still a tiny fraction of billions that were spent on Horizon delivery and firefighting.

This would also be one of the most interesting UX projects in the history of software.

## Transparency

The issues are guaranteed to arise when shipping such a system - and apparently a helpline was established to help with those. In addition, a lot of hidden firefighting took place, trying to reconcile user data behind the curtains - and often failing badly.

None of these had to be hidden from the public.

Yes, billions were spent on the project. Yes, the software is not in a great shape. All of this should've been highlighted by the engineers, and then propagated to the affected users.

A few good principles to follow when you are on support line:

* Don't blame the user. This is an easy path, and often you'd really want to claim that "you are the only one affected" and "try switching it off and on again". Especially if you are an overworked on-call employee with a quota to hit, but even moreso if you are given specific guidance to blame it on a user. I must also add that working on support is an ever-growing backlog of confused and often angry users, and it is an incredibly tough job.
* Aggregate and escalate. Similar issues must be aggregated with automatic escalation of a severity of an ongoing incident.
* All incidents, but especially the ones affecting users or their data must be publicly reported. A write up of a timeline, what exactly happened and how this was mitigated. If a material loss was incurred for users, get in touch and provide compensation.

## Lessons learned

Do we really learn from large scale government funded IT projects? In the best sci-fi book of 2021 [Project Hail Mary](https://en.wikipedia.org/wiki/Project_Hail_Mary) by Andy Weir  humanity is faced with an extinction possibility, and the alternative is an impossible scientific project that requires coordination of every nation on Earth. The solution in the book was to pick the best scientifically minded manager, give them all the power and get away from their path.

The story of Horizon though - I hope it will be taught in every mandatory project management training.
