+++ 
draft = false 
date = 2025-07-28T01:37:10Z
title = "We Are Developers 2025 - conference in Berlin"
description = "More of a congress than a conference, with 15000 attendees and 500 speakers, some of which were from Lufthansa"
slug = "2025-07-28-we-are-developers" 
tags = ['Berlin', 'conference', 'AI']
categories = []
externalLink = ""
series = []
+++

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/IMG_0554.jpg)

I'm calling this a conference, but with 15000 attendees and 500 speakers it wasn't something I was truly prepared for. It was big, took a good chunk of a massive historical exhibition hub of West Berlin, and offered something like 15 simultaneous tracks in addition to 2 massive floors of exhibitions with their own mini talks and demos. I've been to a similar scale dev events in the US, but Europe would generaly cater to a much smaller scale of homebrewed events. But hey, with everything that is going on over the pond, I'm glad we have Las Vegas scale events at home!

## AI

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/IMG_0534.jpg)

No need to summarise this blog with AI, I can totally do it for you. Agentic AI development tools are here, and if you are not adapting your digital product development to use them, then your competition is definitely doing it so.

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/MCPs.jpeg)

Every other talk was related to agentic AI, and most of keynotes would contain plenty of AI hot takes in the realm of "AI will take all the jobs - from software engineers, product managers, designers, data scientists". Belately a speaker would realise they are talking to an audience made of humans and inevitably add "but not you of course, we will still need smart people like you". Some companies managed to find the balance with "you have to buy your AI agent" and "you get to keep your job because of it".

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/IMG_0541.jpg)

I wrote my personal take on [agentic deveopment](https://alexsavin.me/posts/2025-07-21-agentic-development/) too. If you throw away the selling, this can be the most exciting tool for a capable developer since the invention of compiler.

## Github Copilot evolution

Github did a live demo of an async Copilot agent. You can spin it up today from an issue in a repository with existing codebase, containing enough details to start working. This is really the difference between the original Copilot doing fancy code completion, and prompt engineering last year, when you'd be able to quickly generate code from scratch but struggle to apply the same tools onto the existing legacy code. Today's tools are working on top of the existing codebases by default.

Async Copilot will spin up Codespaces instance, install all the dependencies, and then iteratively work on a problem, while also allowing intervention and redirection if needed. It will eventually create a pull request with the proposed changes. During the live demo it did got stuck a few times and needed some nudging to keep going, but the pace of progress is still incredible.

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/IMG_0544.jpg)

I'm glad to report that Github's sticker game is still going strong, and Copilot stickers were the fist ones to go.

## GenAI security

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/prompt_injection.jpeg)

With big opportunities come big risks and the brand new vectors of attack. It was good to listen in on some SecOps talks and what could possibly go wrong.

Good news is [OWASP is already there](https://genai.owasp.org/), evaluating the top threats and offering ideas for mitigation. Prompt injection is still top of the list, since AI chat assitants are everywhere now, and you are mainly converse in text today. Other new vectors are data and memory poisoning - ways of affecting training data of the model, or the long term memory of the vector space of a trained model, so that it starts returning data that wouldn't be otherwise returned.

Apparently you can still do a prompt with `DROP TABLE` in it, and it might even get through.

## Climate change

A couple of talks touched on energy efficiency of the tech. Some languages are more energy efficient than others, and interpreted languages which most of us are using today are traditionally at the bottom of that list.

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/lang-efficiency.png)

In addition to compute time efficiency, there are also considerations of the transit and storage efficiency. Some radical suggestions would include regularly purging all of your unnecessary data, like old logs.

There are, of course, views that once we get to AGI, it will solve all our climate change issues.

## Lufthansa

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/IMG_0572.jpg)

A few big German tech companies were running their talks, including the likes of Mercedes Benz, Zeiss and Lufthansa. The latter did a talk on Cargo cult, and also the one titled "How to sabotage your software development with agile". With 20+ simultaneous tracks, clickbaity title of your talk is something that would easily tilt the scales in your favour.

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/sync_meetings.jpeg)

As with everything, if you push your agile practices to the extreme, flood everyones calendars with sync meetings, have lots of ceremonies and conventions, it's easy to loose track of what we're actually suppose to deliver. The interesting part was about using topology when designing teams and Conway's law:

*"Any organization that designs a system will produce a design whose structure is a copy of the organization's communication structure."*
*— Melvin Conway, 1968*

Teams topology will be closely replicated in the resulting software - the more siloed the teams, the more friction and separation will be in the resulting solution. This is an argument towards open, collaborative and cross-functional teams, but the interesting part here is the understanding, why it matters. There is also a resulting "Inverse Conway Maneuver" - when embarking on a massive refactoring, you could first refactor the team structures, and the rest will follow.

## Food situation

Had a wrap packed with potato mash, pickles and a hot dog. A total winner.

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/IMG_0598.jpg)

Coffee was a bit of a struggle, until I've realise that plenty of expo booths would lure the visitors with free specialty coffee - this is how I ended up watching brain surgery at Zeiss booth on a massive stereoscopic TV while sipping on my morning latte.

## Usability

A good number of stages were placed around 2 massive expo floors - which presented an obvious problem of noise while listening to a talk. This was solved by providing wireless headphones to anyone who struggled to hear a presentation - while accommodating other onlookers who have stumbled onto a talk but were too late to get a seat.

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/IMG_0574.jpg)

They also had a decent web app with all the essential data, daily agenda, and a built-in planner to pick and choose your talks. Having a plan, and a backup plan is something you have to invest some time into when attending events of this scale.

A bunch of workshops required a mandatory pre-booking - all of them were completely "sold-out". A dedicated day 0 was workshops only, and an expensive AI masterclass from Nvidia - and I've manage to attend the one and only workshop on building smart contracts. It was still fun.

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/IMG_0601.jpg)

Also you could donate your bottles - another thing in Germany when empty bottles are effectively a parallel currency that can be used for funding your new tech ideas.

## Lifehacks

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/IMG_0524.jpg)

Events of this scale can easily be overwhelming. Lots of stages with simultaneous tracks for 9 hours straight, lots of people trying to attend, quality merch to be find at the expo. It helps to have a plan for a day, and then also a backup plan in case you won't find a seat and a standing spot for a talk.

Main stage with all the star speakers was quite spacious though, and I think they only complained once about having to shut the doors when the space was full. This is usually the sad case with big events - even for the main stage you have to queue to see some CEO speaking.

The web app of the event was amazing though. You could plan and schedule all the talks, it would contain maps of the venue, and it would also let you livestream other talks if yours happen to be a less interesting one. Picking seats strategically means often sitting at the isle, so you could rush to the next talk before everyone else.

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/IMG_0556.jpg)

Having breaks is also important! It would be too easy doing talks for the whole day straight, but it's also important to chill and have fun. Two expo spaces provided plenty of opportunities to wander around and let someone else show you their product. If you are after the best swag, go there in the morning, before it's all gone.

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/IMG_0547.jpg)

I missed Tech Twitter for the event - or something that would clearly replace it. The orgs didn't explicitly advertise a choice of a social network or a hashtag. I think there was a BlueSky official account mentioned briefly. The best part of IRL events is of course being able to chat to real people, but this is also a chance for everyone to converge at some online social space - and I'd say you need the orgs today to point to the crowds where to go.

Which leads me to the final hint. Bring your colleagues to the event. You won't see them much - there were something like 7 of us attending together, but we ended up spread all around the conference. We also had our WhatsApp chat going on which talks to attend, sharing plans, and getting together after a busy day to share the learnings with some currywurst.

![](https://alexsavin.me/photos/2025-07-22-we-are-developers/IMG_0533.jpg)
