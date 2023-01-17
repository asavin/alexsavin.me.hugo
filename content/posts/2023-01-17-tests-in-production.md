+++ 
draft = false 
date = 2023-01-17T10:37:10Z
title = "Continuous testing on production"
description = "You can run tests on live environment"
slug = "2023-01-17-tests-in-production" 
tags = ['testing', 'engineering', 'delivery']
categories = []
externalLink = ""
series = []
+++

*TLDR: You can run tests on production. It's the ultimate integration test, but there are a few rules to follow.*

Software delivery is always full of compromise. You either ship it (slightly) untested, or you don't ship it at all. 

There are a number of practices that are considered good and increase chances of your uninterrupted night sleep. It is generally a good idea to write tests. It is also good to run them before shipping things to prod. Ideally there are no failed tests. Ideally you can run tests and deploy changes before someone else merges a new change on top of yours. Ideally you can isolate the change you want for prod from the rest of the incoming changes. Ideally when you ship, things don't break.

You could classify all the activities that boost your delivery confidence into two categories:

1. Pre-release
2. Post-release

A general convention is, that if you have enough gatekeeping in the pre-release stage, you can largely skip post-release activities. Sometimes this is taken as an unwritten belief. We've spent a bunch of time writing all these tests and doing the CI pipeline with reporting - surely now things are good enough?

Truth is, even with the 100% code coverage (which is rare, and also - unreasonable) you would rarely cover all possible permutations of the user input. Which, in turn, affects state of the system. Which creates unpredictable scenarios that were never tested for. 

Which leads to things exploding.

Release pipeline is always a trade off. We have to be able to build and test within a reasonable time. If your test suite takes a few days to run, sure that might provide better coverage. But that will slow down the release process to a snail pace. The motto becomes "fail slow and break things". 

Not ideal. 

Traditionally you'd have comprehensive unit tests, some integration tests and a suite of e2e smoke tests - covering the core scenarios, but not much else. Releasing becomes possible, edge cases rely largely on unit testing, and all in all this is a valid approach for most products.

We could also complement this with continuous tests running **on production**.

Once we are on prod, things don't have to be lightning fast. We can have comprehensive e2e tests running for real, trying every possible permutation of user scenarios. Ideally, also performing a good clean up and keep the system state affected to a minimum. It doesn't matter if test run takes a few days to complete. We are always running against the most recent version of the system that is actually exposed to our users. Any regression encountered is a legitimate issue.

We can now use scenario factories and generate tests to cover for more permutations. Sure, it'll take more time to run - but now this is not blocking anyone, and can take its time. In fact, you could throttle down the execution of the tests, to keep the load to a minimum. Maybe throttle up if there are known time windows while real users are asleep.

A few companies I used to work for used this approach. You'd have production tests running constantly, 24/7. If something breaks, that would often trigger a PagerDuty event. Sometimes that would mean a copy change that snuck through the release pipeline. Sometimes that would be an intermittent service availability issue. Sometimes that would be a legitimate regression that was not caught otherwise.

Production tests do require a certain discipline. They cannot affect experience of your end users in any way. Data clean up could be a challenge since e2e tests rarely guarantee successful cleanup after run. You might not be able to re-purpose existing tests, and will have to maintain *yet another* suite of tests. And of course, failures on production should be properly reported and handled - which implies some level of on-call team dedication.

Side note - if you are not in a position to commit to a proper on-call - you might be able to introduce a [Tiger Team](https://en.wikipedia.org/wiki/Tiger_team) rota. This is effectively on-call, but run across org and traditionally only during work hours. This does mean you'll have to dedicate _some_ team capacity - but that is always the cost of maintenance, which is proportionate to the amount of software you have shipped.

### Footnote

This article was hand typed by a human, and no AI was used in making of this blogpost. I used to run things through Grammarly before publishing, but at this point I'd be inclined to keep the mistakes in - that's something that humans do and computers don't.
