+++ 
draft = false 
date = 2026-06-11T01:37:10Z
title = "Living on a token budget"
description = "Tips when tokenmaxxing lifestyle is not easily affordable"
slug = "2026-06-11-living-on-token-budget" 
tags = ['AI', 'Claude Code']
categories = []
externalLink = ""
series = []
+++

Unlike a few lucky engineers enjoying tokenmaxxing, most of us are living within the constraints of a token budget. It might be small, it might be big, but it is likely there somewhere.

As tokens are getting more expensive, ability to live and deliver within the budget will probably be the leading topic in hiring interviews. Here are a few hints, some more obvious than others, that help me month to month with minimising token usage while having some kind of a meaningful output.

## Know the difference between input and output tokens

Input tokens are what you are inputting. Prompt, a file, an image. Output tokens is what a model prints back.

Input tokens are 5x cheaper than output tokens. Longer prompts with better context, better task setting would generally mean less thinking and better output.

It's cheap to provide lots of context to the model.

## Keep an eye on a current model

If you are using default tooling, it will try and default onto some kind of latest and greatest model. Both Claude and Gemini are known to do that. A top tier model would easily burn through the monthly budget in a day, if left unchecked.

Additionally, models now have effort levels - low, medium, high and MAX. Even a cheaper model on a max effort setting would quietly consume more tokens.

Most tools allow hardcoding of the settings, but this is something you have to do yourself. It is not, strictly speaking, in the best interest of a vendor that you'd always default to an old and trusty model.

## Preserve context

During a session with an agent useful outputs will occur. It is worth saving it, and not rely on the context window.

First off, a context window is capped, and eventually will overflow. This will result in compacting, which will inevitably loose some details of the conversation.

Secondly, long running session cost input tokens.

Start a Notion document along the session. Or a local markdown file. Or a Miro board. Though Miro API is not amazing, and for me Claude been struggling when updating large Miro boards. As the session progresses, ask an agent to update documentation, especially on conclusions and decisions.

You could even start a JIRA ticket and keep it updated as the research progresses. I would often start a feature refinement session with Claude, gaining insight and updating implementation plan, often across multiple JIRA tickets, combined into a single epic.

Next day you could start a brand new Claude session, point it to the previously created ticket and ask it to implement it. At this point you can use the cheapest model on the lowest effort level - all the details would already be refined, with detailed step-by-step instructions.

## Build re-usable tools

Agents are very eager to offer help and to action things. If you let them, they will run every single command in terminal - and charge you for it.

If the nature of tasks is repeatable, instead of asking an agent to do the work, I can ask it to build me a shell script. Or a Python script. Something that I can run then myself, for free.

Shell scripts are especially useful. Bash scripting is incrediby powerful, allows input arguments, and you can build them with Claude in no time. Claude will gladly debug it too, until it is working exactly as expected.

Build many small bespoke tools, and use them for your benefit. No tokens needed.

## Run retrospectives with your agent

After a particularly complex session, where things were discovered, and ways of working were optimised - it is worth running a retro session with an agent. What went well, what went wrong, what can we do better next time?

Where did we spend the most tokens this time, and how to avoid this in the future?

Learnings are then committed to a long term memory, or to a project specific memory. This is very much like training a colleague - establishing ways of working, reducing waste and optimising for cost.

## Kill long-running sessions

It's easy to just leave a session running, often across multiple days. Context window will overflow eventually, but then compacting will kick in, and the session continues. Today even when you are terminating a session, Claude will helpfully provide you with a session ID that can be used to resume it at any point.

Don't do it.

I mean, sometimes it is worth it. But if you are documenting discoveries, distilling useful context into JIRA tickets and Notion, there is no reason to keep the session running beyond a single working day. This cost plenty of tokens that could be better spent.

Run small, focused sessions, document all discoveries and terminate that session.

## Be very specific and provide entry points

If you are vague in task setting, and the codebase is massive, your agent will gladly go over many files, while trying to build the "full picture". Chances are, you already have this picture in your head. Providing exact entry point to the agent would save a lot of time and tokens. You could even point to exact line ranges if a file is particularly large.

Do:

"We need a change in myUserComponent.tsx to remove obsolete feature flag my-legacy-feature."

Don't:

"Could you check if we have obsolete feature flag something like "legacy feature", and remove it across our app?"

## On tokens

What is even a token? Are 2 tokens equal?

You might think a token equals to a single character from model perspective. In the past we used to have such models, but for LLMs one character is too small. A token is more like a syllable, which can be combined with another syllable and make something meaningful together.

Each model uses something called "tokeniser" - something of a massive dictionary that breaks all input into tokens, and translates all output into human readable words. Things will be even more interesting for models that create images or compose music, something worth keeping in mind.

There are a bunch of different tokenisers, and every model vendor would use their own, often a proprietary one. Which means all tokens are different, and can mean very different things depending on the model and the context. Charging by tokens is like Apple charging by storage capacity of an iPhone - very much a proxy way of introducing different pricing tiers, and not directly representative of what you are really paying for. I wouldn't be surprised if the industry moves onto some kind of "reasoning effort" unit going forward - something that reflects the actual "thinking" involved to produce an output.

But for now, we are stuck with token budgets.
