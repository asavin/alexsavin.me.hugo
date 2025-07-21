+++ 
draft = false 
date = 2025-07-21T01:37:10Z
title = "Agentic development"
description = "Prompt engineering is a thing of the past, agentic development is the present"
slug = "2025-07-21-agentic-development" 
tags = ['AI', 'agentic']
categories = []
externalLink = ""
series = []
+++

If I had to pick one takeaway from the massive dev conference in Berlin last week it'll be - adopt agentic product development or go out of business.

It might not be that dramatic if you are a massive corporation with a unique know-how, or if you are in a unique business niche. But for a generic product company it'll be exactly that. Agentic development, end to end, from product specs to implementation and deployment. It's not really somewhere in the future, it is our very current present, and your competition is already using it daily.

An agent is a piece of software that utilises underlying AI models to simulate a professional. Could be a software engineer, could be a product manager, could be a QA engineer. Could be a data scientist, data engineer, devops engineer. The list goes on. The original focus was on replacing software engineers, but now it has expanded to pretty much all aspects of digital product development. Is it even limited to digital? Probably yes, for now. An example could be the current iteration of GitHub Copilot, or Claude Code. Something that takes requirements and produces a working solution of a production grade.

An example from the conf was Windsurf IDE - which was able to fetch designs from Figma, look at the existing codebase of a frontend app, and implement a solution in asynchronous fashion.

If you are, like me, somewhat behind the curve - here's the current misconceptions and the state of things.

## Agents are only good with greenfields projects

This was true last year - agents would generally be good at quickly prototyping apps from scratch, getting something rudimentary working in a minimal amount of time, then struggle to maintain the existing codebase. They would also struggle to take in massive legacy repositories with 100k+ lines of code, and files beyond 400 LoC.

Today's models have no problem with any of that. Context window is now well into millions of tokens, meaning it can read through a massive legacy codebase, figure out conventions and implement new solutions on top of that.

## Agents are only good at coding

Apparently Google is now hiring Product Managers expecting them to use LLM driven tooling to produce product definitions and requirements. There are tools that will generate human readable documentation out of source code. Ages ago I was building a custom integration that would fetch documentation out of markdown comments in source code and produce Confluence documentation. This is a solved problem now - furthermore you have options to keep your truth in a code repository, or have it vice versa in a readable format and produce business logic out of that.

## Prompt engineering vs agentic development

2024 was all about prompt engineering. This is not the case anymore - it seems that you don't need humans to write prompts. And also prompts are not enough anymore. You are more of a product manager now, figuring out the needs and specs of a product, and then giving directions to a herd of agents. As an engineer you might also be building agents for a specific task.

## MCP

It feels like Model Context Protocol came out of nowhere and is now a standard of how models can communicate with the rest of the world. There are a bunch of MCP based integrations now for all kinds of existing services and data sources, and the list keeps on growing. This is what makes agents so powerful, and honestly reminds me of the days when we discovered public REST APIs and how you can expose them for everyone to mash up new web applications.

## Tools

So many existing tools. We truly live in the interesting times.

GitHub Copilot - started as a fancy code completion tool, but now went full async agent. Today you can create an issue on the existing Github repository with the description of the job to be done, and unleash Copilot agent on it, which will spin up a Codespaces instance and start working on the change.

Claude Code - going the command line CLI route. You run it on your machine, and it will work on your app, using tokens from a model of your choice. Anthropic says the average dev will consume about $6 worth of tokens a day - or there's a monthly subscription too.

ChatGPT Codex - also an async agent that you link with your Github account. Included in the Plus subscription.

Google ADK - an Agent Development Kit, to quickly get you started on building your own agents. Config driven, model agnostic, infrastracture agnostic.

n8n.io - workflow automation that also allows agents development, with MCP connectors. Fully visual UI, no coding experience required.

Windsurf IDE was quite prominent in the event space, but with the recent developments it looks like the IDE itself might be going out of business any moment now. Luckily there's plenty of competition, including Cursor IDE.

## Next steps

Engineers tend to optimise and automate things, so that we get to focus on the interesting work. I hope we could steer agentic development in that direction, while focusing on the kinds of problems that have no obvious solutions yet. Who knows what the future brings?
