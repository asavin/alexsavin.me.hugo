+++ 
draft = false 
date = 2024-10-29T01:37:10Z
title = "Listen to the engine noise"
description = "Is your locomotive feeling healthy today?"
slug = "2024-10-29-listen-to-engine-noise" 
tags = ['software', 'delivery']
categories = []
externalLink = ""
series = []
+++

![](https://alexsavin.me/photos/2024-10-29-engine-noise/locomotive.jpg)

Sometimes getting your change all the way to production feels like crossing a finishing line after a marathon. Massive fanfares, you've made it all the way to the user. Time to get a cup of tea and pick up next JIRA ticket.

When a company is small, or tech stack is young, or all of the above, pushing changes to live is a breeze. No one yet discovered [Husky](https://typicode.github.io/husky/) git hooks, or had time to set them up. Build pipelines are extremely basic - doing the job, but not much more. There might be _some_ tests, but not a huge amount. The product itself is small and doing just enough.

At that point being able to quickly iterate on production is a must - there will be critical fixes to ship, missing features that users demand, and newly discovered state regulations to be addressed. We are in full founder mode - move fast and break things, but then fix things and keep moving.

Assuming the product does ok - and there's enough runway to keep building - things start to scale up. Engineering team goes from 2 to 200. You have operations and customer support teams. More features are shipped, and your userbase is going 1000x. Founder mode is getting replaced with long term marathon mode.

At this point you've set up your linting, git hooks, unit tests, integration tests, there's hopefully some kind of smoke testing going on across all environments. Automated alerts, PagerDuty, on-call rota, Grafana dashboards. UI end-to-end tests and HotJar to detect rageclicks.

This is usually the time when production releases become slow. You git hooks will slow down commits. Test coverage tool will shout that you've added a bunch of code but not so much tests. Writing tests might require diving into the world of fixture generators that someone before you set up and since left the company. By the time you've made your change all the way to production, it might legitimately feel like you are finishing a marathon.

And there are smoke tests and HotJar to tell if things are doing fine on production - so nothing to worry about.

Well, everyone got a plan for a good feature until it meets its first real life user. You only know the change is good, when you have observed it in production for a few days.

One way of observing that is looking at production logs. Matrix style. I'm actually surprised we are not doing more of this. And it is tempting to say that you could feed all the logs to LLMs or tools, and let _them_ figure things out. That is also useful - in addition to observing logs as is.

Observing production logs is the zen of software engineering. It's the literal equivalent of listening to the car engine running. You can tell a lot about its health just by listening to the noise.

Even when everything is working just fine with no errors, observing logs is extremely useful. You might spot early warnings of a 3rd party API getting deprecated soon, a library towards the end of its life, performance hints or something working in a completely different way that you'd expect. Live users also tend to use software in the most unpredictable way with the least expected data. Skip unskippable fields, add numbers instead of strings. Nulls, nulls everywhere. Things might still work, but only because a safety feature managed to convert your `null` into an empty string at the very last minute.

Observing it might actually be tricky. Access to production environments is often limited - or shut down completely. User sensitive data is everywhere in production - databases, storage buckets, and it does tend to leak into logs too. Solution to that is to lock down access to prod for everyone but the key SRE team.

I would argue that it is extremely important for engineers to observe the feature they implemented in production. Release to prod, observe for a few days, learn. Once your change is facing real world, only then you can see if it was implemented correctly. And yes, it might work perfectly in all the staging environments and pass all the tests that were written for it - and still fail in production. 

In fact - big fails are easy to spot and usually there's someone who will shout about it. Quiet fails are the ones that are much more dangerous. A quiet fail can run for weeks or months without being noticed, cost millions in damages, and is  totally capable of bringing companies down.

## Footnotes and attributions

Headline photo is [Silverton Steam Train, Silverton Colorado](https://flickr.com/photos/a_little_brighter/54087207815) by Harold Litwiler. Used thanks to Creative Commons license.

GCP got a [handy tool](https://cloud.google.com/architecture/manage-just-in-time-privileged-access-to-project) that allows temporary privilege escalation when you need access to production. It solves part of the problem - when things are on fire, at least there's a mechanism to provide you with access to the burning building. It is not going to solve the part when an engineer observes a working engine on production and discovers quiet failures.

