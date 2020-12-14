+++ 
draft = false
date = 2020-12-14T18:01:30+01:00
title = "Upgrade to Hugo"
description = "Upgrading my blog to a new modern engine"
slug = "" 
tags = ['hugo', 'indieweb']
categories = []
externalLink = ""
series = []
+++

It is time to migrate my self-hosted standalone blog to a more modern engine. This engine is going to be Hugo - a super fast static site generator, which is also super friendly and highly customizable. It might also push me towards learning Go, but we'll see about that.

The original engine this site was running on was a bespoke generator written in LiveScript language about 7 years ago. I've written quite a lot of functionality around it, so the whole site was pretty much homebrew LiveScript, running on Node 0.10. It was long time ago. Eventually things broke, and this time instead of tweaking things back into functionality I've started looking around for more shiny generators. Something that I wouldn't have to support. Something that would still take a bunch of my markdown files and turn them into a website. Minimum efforts, maximum usability.

Hugo in the end turned out to be just that. You give it a bunch of markdown files with all your precious blog posts, and it turns them into a fantastic looking website. It is a config driven development, meaning the most programming I had to do was making a [config file](https://github.com/asavin/alexsavin.me.hugo/blob/main/config.toml) that would produce a desired result. That, and picking a great looking theme.

Everything is alive and well, but a few things I had to sacrifice for now - and I might put some fixes later:

* The canonical URL:s for old and new blog posts have changed now. Old links will still work, however the new blogs will be under `/posts/[date]-blog-title/` url:s with no `.html` at the end. The last bit is kind of sad, as this was a thing that separated original document based websites from the web apps we know today. Every page was an html page, as was indicated by the extension in the URL.
* RSS feed is still available, but the new route is this: [https://alexsavin.me/index.xml](https://alexsavin.me/index.xml). It makes more sense, and probably is more easily discoverable. Previous incarnation of the site contained support for two languages, and two separate RSS feeds per language.
* The site is now single language - meaning I gave up on the idea of blogging in both English and Russian. The idea was great, but in reality I have barely capacity for blogging in on language.

So here we are - a shiny new site, powered by a (hopefully) well supported static site generator. Now with technical details taken care of, we'll see very soon if I'll start posting more.

## But why not just use Medium?

Couple of reasons. First - I've already had an archive of blogposts from the past in markdown, with images and everything. Pure content, compatible with most static site generators, but not compatible with Medium or similar hosted solutions. Some of those posts are still getting regular hits, and it would be a pity to take it all down.

Second - I'm still not entirely comfortable with a thought of someone else owning my content. Eventually the Internet will be consumed by hosted solutions, but at least for now I still like to pretend we live in the era of independent sites where you can build whatever you want and host it yourself. The content exists on my local machine and Github, and can be migrated easily to any internet bucket out there.

So here we are - still a self hosted site, under a personal domain, generated with the power of Go. Don't forget to subscribe to my RSS feed.
