+++ 
draft = false 
date = 2024-02-08T01:37:10Z
title = "Develop software like it is 2003"
description = "What do you mean there is no StackOverflow?"
slug = "2024-02-08-programming-in-2003" 
tags = ['software', 'nokia']
categories = []
externalLink = ""
series = []
+++

![](https://alexsavin.me/photos/2024-02-08-nokia-software/nokia-3650.jpg)

My first job out of uni was working for the hottest company in the world. In 2003 FAANG was mostly AG - Apple was sort of around, Google was doing web search and not much else. And back in Finland, we've had Nokia.

Nokia has been around since the 1800s and is still around today. But 2000 to around 2009 were undoubtedly Nokia's golden years that it is remembered for today. As I was finishing my degree, Nokia was hiring every computer science student out of the doors, trying to massively scale up. The opportunity was there - smartphones were the hottest topic. 

So, pour yourself a cup of strong *Juhla Mokka* coffee. It's year 2003. Nokia just released its first-ever camera phone. Lord of the Rings movies are coming to cinemas every year. AI only exists as a plot in horror sci-fi novels.

![](https://alexsavin.me/photos/2024-02-08-nokia-software/nokia-7650.jpg)

What it was like developing software back then?

## Version Control

[Continuus Synergy](https://en.wikipedia.org/wiki/Rational_Synergy)

Git was not really around, GitHub did not exist, and software versioning was largely optional and only required once you finished your work. Synergy was the tool, with no CLI, and only a GUI that was incredibly slow and unintuitive to use. Originally developed by IBM in 1990, which might explain some of its quirks.

![](https://alexsavin.me/photos/2024-02-08-nokia-software/synergy.gif)

By now we know that every version control would introduce a unique vocabulary - and Synergy was no exception. I was afraid of using it - only keeping to the well-known path. In the unlikely event of a merge conflict, a specialist would be called upon - and would take over the conflict resolution. It was a hostile app, very fragile and incredibly slow at the same time.

For the slowness, looks like we have the answer now:

> It was decided that a compiled language such as C++ was not sufficiently flexible, reliable, and productive, and so a new programming language called ACcent was created. ACcent has many features similar to Java, but pre-dates it by five years. It has a compiler that compiles to machine-independent byte-codes, and a virtual machine execution environment with automatic memory management.
	
Tortoise SVN would be introduced as an alternative much, much later - and it was a breath of fresh air. Around 2009 Nokia also acquired a company called Qt - and being the open-source friendly C++ framework, they already used Git. But Git never got any official adoption.

## Notion in 2003

The idea of a web platform for documentation and literally anything else is not new - and most of you would name Microsoft SharePoint being there early on.

Nokia used [IBM Lotus Notes](https://en.wikipedia.org/wiki/HCL_Notes).

![](https://alexsavin.me/photos/2024-02-08-nokia-software/Lotus-Notes.jpg)

It was likely a revolutionary product back in 1989 when it was introduced. A network-based app that could allow document creation and hosting, custom apps, workspaces, email client and even something resembling an intranet with its navigable pages. Everything was remotely stored and retrieved, kind of like with web browsers. Unlike with web browsers, every user action would also have to reach the server first. Once you click on a loaded form to input a value, it could take a few seconds for a blinking cursor to appear.

It was slow.

Lotus Notes were our Notion, JIRA, SharePoint and user feedback forms all in one. This is where roadmaps would be planned, and bugs would be reported. I could see the former glory and power of the system but would try and avoid using it unless I had to - which was daily. Do you know the feeling of an app when you think hard before making any user actions? This was one.

Lotus Notes were used throughout my time and never deprecated. The only alternative then would be migrating to SharePoint, which at that point would cost way too much for a company losing its revenue to iPhones and Androids.

## Continuous Integration

CI was a floor of people - literally a team of engineers. They were called the Integration Team.

Jenkins did not exist, Version Control was Synergy - and most of the testing was a bunch of manual QA:s - I was one of them for the first year or so, before upgrading myself to the role of a software engineer.

A floorful of engineers would daily collect source code updates from every team and attempt to build a flashable image for our current hardware platform. Remember - no unit tests, no integration tests, and _some_ manual QA - mostly based on the builds produced days earlier. All of that meant that the integration team was at the front of a shitstorm.

Builds would fail often - and the team would scramble to find issues and fix them. This could require chasing relevant teams that produced unbuildable code. Luckily everyone sat in the same building (more or less), and chasing often was quite literal.

When the build was successful, a smoke test would run. For daily builds smoke test was exactly that - can we boot the phone, and would it make smoke in the process? No smoke, successful boot - ship it.

For weekly builds a team of QA:s would manually run through the scenarios and attempt to find issues - which were plentiful.

Major releases would involve top management signing off on the known bugs and giving it a big thumbs up - before the image would be shipped to the factories and flashed onto millions of phones.

## IDE

All computers were Dells running Windows 2000. An obvious choice for an IDE back then would be Visual Studio of some kind. Microsoft had the best IDEs even then, and Visual Studio was very flexible, allowing for custom workflows and languages outside of Visual C++ and Visual Basic.

We were developing for Symbian C++, with a custom build pipeline and its own simulation. Think iPhone Objective C development, but for Nokia phones. Visual Studio was the official IDE for Symbian initially - and things were very good. C++ is a compiled language with strict typing - which becomes _extra strict_ with Symbian. If your app is building, there's a good chance it would run fine too. You could run it on a simulator, with breakpoints support. And most of us had experience with Visual Studio since this is what all the unis would teach us too.

Very quickly though Nokia pivoted to [Metrowerks CodeWarrior](https://en.wikipedia.org/wiki/CodeWarrior) and abandoned Visual Studio support.

![](https://alexsavin.me/photos/2024-02-08-nokia-software/CodeWarrior_IDE.jpg)

Interestingly CodeWarrior was initially a Mac app - an IDE for microcontrollers and CPUs. This choice would make sense if that would be our target, however smartphone software - even on Symbian - was very different in nature.

CodeWarrior was largely pushed onto everyone, and it was not great. Very unintuitive, not meant for the job, with a different set of conventions - most teams tried to hold on to Visual Studio for as long as they could. But eventually, everyone was pushed onto CodeWarrior.

With CodeWarrior, there was a moment of sunshine when you could hack an on-device debugging. Code would run inside an IDE, connected to real hardware - with breakpoints and a memory stack. It was flaky though - I was one of the few who managed to get this working - and it was working _most_ of the days.

And then Nokia bought Trolltech's Qt framework.

Qt was actually nice. Great framework, lots of documentation, and fantastic tools that were also built using Qt. Nokia also was a bit late. 5 years earlier it would revolutionise everything - devs would love it, and Symbian would be the platform for great apps. In 2008 iPhone was already out, and Nokia was trying to make bold moves to lure app developers onto a platform that was now perceived as a legacy one.

Around 2010 a decision was made that _all software_ at Nokia would be made with Qt C++. I worked with Qt Studio, and also QML got introduced. Let me say a couple of words on that.

Qt C++ is a great framework, but it is still C++ we're talking about. Not everyone considers C++ an easy and friendly language. This is where QML shows up. QML was a JavaScript-based framework - think React but for native mobile apps. Well, ok - React Native. But 5 years earlier. And for Nokia phones only.

QML was genuinely nice. Since it was JS-based, you could have your app running in a Symbian simulator - which took _ages_ to boot. And you'd have hot code reload. Tweak your app, and have things updated right in front of you. This was unthinkable - at the very least you'd always have to rebuild your app for the simulator. At the worst, you had to rebuild a hardware image, flash it onto a phone and try things again and again.

## StackOverflow

...wasn't a thing in 2003.

What you've had is:

* Official documentation
* Co-workers
* Books from O'Reilly
* Random internet forums

Language-specific problems were less of a problem, since IDE:s would highlight and catch those before the app is built. Oftentimes you'd have a blank page problem - when you wouldn't know even where to start. GitHub wasn't a thing either, so you couldn't simply find some open-source apps and see how they were made. But we've had a huge internal codebase of _every single app_ bundled on your Nokia smartphone - and that was actually highly useful. You could also track down a person who wrote it, and walk to their floor for a cup of coffee.
