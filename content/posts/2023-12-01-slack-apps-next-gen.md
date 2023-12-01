+++ 
draft = false 
date = 2023-12-01T01:37:10Z
title = "Next gen Slack SDK - DX and first impressions"
description = "Deno, Typescript and hosted Slack workflows"
slug = "2023-12-01-slack-apps-next-gen" 
tags = ['deno', 'slack']
categories = []
externalLink = ""
series = []
+++

![](https://alexsavin.me/photos/2023-12-01-slack-next-gen/wires-lamps.jpg)

I've been playing with the [new Slack SDK](https://api.slack.com/automation) - based on Deno and Typescript. It's good.

Up until now you'd use REST API to build your Slack apps. Sure, there might be a library in your native stack, but under the hood it would still be the same http calls to the same API. Often, quite a lot of those. A complex app would be like building a ship in a bottle - bunch of requests and interactions via the bottleneck of this API.

This sort of changes now - you can build a complex workflow, and deploy it straight to Slack. It runs natively in your workspace - and on Slack servers. There are native functions to call, and even a NoSQL database, if you need some persistence.

Sure, workflows were sort of meant for a different purpose. Like Shortcuts on Mac, you build automation, combining steps into something meaningful. There's even a UI based workflow builder in the Slack app itself. The traditional API based apps needs to be declared as such, and could also be distributed in the Slack's own app store. Not the case with workflows - these are meant for "personal" use - or at least within your Slack org.

Which is, to be honest, all I need. Custom integrations, private to the org, fast to run and easy to build. And yes, hosted by someone else.

I've spent a few days now tinkering with Slack's Deno / TS SDK, and here are some dev notes.

## SDK and CLI

You will need [Deno](https://deno.com/) - which is like Node.js but properly built. I've heard about Deno, and it is truly excellent. Typescript out of the box, security model, testing, linting, and Rust under the hood.

![](https://alexsavin.me/photos/2023-12-01-slack-next-gen/slack-create.png)

Slack CLI runs on Deno, and can:

* Scaffold your brand new Slack app
* Run the app locally
* Scaffold new triggers and custom functions
* Deploy the app
* Check on deployed app logs
* Delete deployment

## The app structure

All apps are made of workflows, triggers and functions. Last two are optional. All written in Typescript.

* Workflows - main blocks of the app. This is where you define the structure of the flow, with steps and I/O. You could also use built-in functions, and contain all of it within a single workflow.
* Triggers - ways to trigger the workflow. Could be an external webhook, could be a timed schedule. You can also listen on internal events, or have a shortcut that becomes alive when pasted into a Slack chat.
* Functions - custom logic, think of lambda functions.

## Hot reloading

You can run the workflow locally with `slack run` - which is very cool, since it provides all the connectivity to your Slack workspace, while still running the app on a local machine. For workflow TS files you get hot auto-reload out of the box. 

It might be tempting to assume that this applies to triggers and functions too - but no, you have to re-create those manually. This is likely to change though, unless there's a fundamental reason why they can't be hot reloaded. For now every time you update your existing trigger code, you have to re-create it with `slack trigger create` command (and likely the same for custom functions).

And of course, don't forget to update triggers _both_ for local, and for remote deployments!

## Rate limits

With a webhook trigger you can hit your workflow from outside. While it might seem like they don't enforce rate limiting on those requests, it is officially declared as 10 requests / minute. I've got in touch with Slack support, and they clarified further:

* Indeed, 10 requests / minute / workflow
* If you have multiple workflows in the same workspace, rate limiting is still _per workflow_
* You will get 429 errors when exceeding rate limits

## Shortcut triggers vs Webhook triggers

Shortcut triggers will produce a URL, but clicking on it will lead you to a 500 error page. Not too friendly.

![](https://alexsavin.me/photos/2023-12-01-slack-next-gen/slack-500.png)

Instead, the expectation is to copy / paste this URL into a Slack conversation. This is when the magic happens - this shortcut is suddenly transformed into a workflow start button. Pressing this button can trigger, among other things, an interactive form - all within Slack.

![](https://alexsavin.me/photos/2023-12-01-slack-next-gen/slack-play-button.png)

Webhook trigger URL is, of course, a classic webhook - you can hit it from your Postman, and no extra auth is required. Not sure if this is good or bad - the URL is long and complex, but also if it leaks, anyone could use it. On the other hand, it is easy to delete and re-create webhook URLs, so you _could_ have a rotation going if neeeded.

## Secrets handling

`slack env add` - very straightforward

## Using of CI for deployments

`slack deploy` is cool, but can we use Github Actions or CircleCI for app deployments? Totally - there's a very decent example of how a [Github Action](https://api.slack.com/automation/cli/CI-CD-setup) could look like for both app testing && linting, as well as the actual deployment.

## Cost

You have to be on a paid plan, but otherwise running workflows is free right now. Unless you have implemented custom functions. 

You will be charged for running custom functions - there's a free tier of around 1000 runs right now, and after that it'll cost 5c for each run.

I wouldn't be surprised if Slack will start charging _per workflow run_ at some point - once we've built a bunch of those are are completely hooked.

## Final thoughts

In terms of functional Slack native apps this is huge, and will improve a lot both dev experience and user experience. No more need to use http API calls for every tiny action - things can happen natively within the workflow. Great capabilities to integrate with 3rd party services via connector functions, as well as your own cloud hosted apps. Solid choice of tech stack with Deno and TypeScript - with built-in testing and linting.

Will Slack become the next SharePoint? Sure. But at least we get nice responsive apps and good runtime. Now, somebody endorse me for my Slack skills on Linkedin.
