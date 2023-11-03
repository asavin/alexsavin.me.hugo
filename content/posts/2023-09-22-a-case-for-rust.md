+++ 
draft = false 
date = 2023-09-22T06:37:10Z
title = "A case for Rust"
description = "What if web apps but reliable and fast"
slug = "2023-09-22-a-case-for-rust" 
tags = ['rust', 'web']
categories = []
externalLink = ""
series = []
+++

For the past 10 years, I've been mostly writing JavaScript.

Don't get me wrong - it pays quite well. And yes, sometimes it would be TypeScript. Or LiveScript. Or ECMAScript. Transpilation became a trend. Abstract Syntax Trees became a hot topic.

But it was always you, JavaScript. And the reason - you run in a browser.

Other languages always existed, but none of them could be natively run in a browser. And we all knew JavaScript is not a great language. Scripting languages rarely are. As a script, you don't really have much access to the underlying resources. You are supposed to tell the runtime what you want, and it wouldn't even trust you to run it.

For some newcomers to the software industry, it might seem to be the default. Your app is merely a script. Your UI is interpreted. You have no power over resource usage. And everyone in the industry seems to be doing the same thing over and over again, so surely this must be right.

And I feel like with Rust things are changing now. For much better.

## How much better

NodeJS was revolutionary. At last, you could use the same JavaScript not only in a browser but also backend. Hiring in tech has never been easy, but now you can lower the language proficiency to just JavaScript. Have the same chunks of code running both front and backend. Have the same toolsets.

Some renegades kept on running backends on C#, Java and Python. This was slow. Not the languages - the execution. Different teams would be involved, and to get a vertical change shipped you'd have to plead with multiple teams to work together. This takes time, and competition eats you alive.

Speed of delivery is, still, everything. Only second to the quality of delivery.

## Assembly

Web browsers were never meant to be doing what they are doing today. We, the developers, demanded to render massive websites, with interactive elements, animations, and smooth scrolling, at 60+ fps. Browsers offered HTML and CSS.

With JavaScript and DOM, you could manipulate every element on a webpage. With shadow DOM and React, you could even have some convenience doing it. But still not fast enough. 

What is fast enough? Assembly. Direct manipulation of CPU resources. No interpretation, straight to the business. Assembly used to be _the language_ when you needed speed. It also gave you absolutely no guiderails, so it was too easy to make your computer smoke and sparkle. But hey, that's like riding in a Formula One car.

Eventually, browsers gave up and introduced Web Assembly. You supply a binary package that is interpreted by the `wasm` runtime in the browser. This is still not exactly a direct interface to your CPU, but quite possibly the next best thing. After all, there are lots of CPU types to support, and why not let browsers handle that.

But the most important thing is that a binary executable can now be run both frontend and backend.

## Rust

Rust has been around for some time now. Mozilla used to endorse it, claiming Firefox is so fast because they rewrote the rendering pipeline in Rust. It is a statically typed language, akin to C or C++. Compiles to native binaries, which are very, very fast to run.

It is perceived as a system-level language, and why would you even consider something like that for web development? Surely we need speed of delivery, dynamic typings and human readability?

## Stability

With script languages the future is vague. 

A JavaScript app describes what it wants, with runtime doing its best to run it. It is entirely possible that the app would crash. Or express an unexpected behaviour. Variables are dynamically typed and coerced when runtime requires that. Memory is allocated on the spot - and if that fails, your browser tab becomes unresponsive.

When exposed to a user, there are no guarantees for a JS app. And I feel like we're mostly used to it. If a webpage is broken, reload the whole thing. We use services that collect JS errors on frontend _after_ they have happened.

With statically typed languages the story is very different.

It is as if you could _guarantee the future_.

User experience is often cited as one of the key features of successful products. Users do want features, but they also want them to run quick, and not crash in the process.

If only we could write apps that would never crash.

Rust can help with this. Sure, a Rust app can crash - but you can catch most future errors during the compilation.

Rust compiler is incredibly powerful. In JS we use linters and transpilers with "pretend" types to try and catch possible issues. All of those are unnecessary when you can have a solid compiler.

Rust compiler will only produce a memory-safe binary - and will refuse to do so until you have addressed all the possible memory usage issues. Rust is so confident in its memory model that it has no garbage collection. If your app compiles, you get a cookie and a reliable app.

## Reliable universal web apps

Rust on frontend via WebAssembly. Native Rust-compiled binaries on backend. Now you are playing with power.
