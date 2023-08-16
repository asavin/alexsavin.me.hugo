+++ 
draft = false 
date = 2023-08-16T10:37:10Z
title = "Sandboxes and why they matter"
description = "Move fast with sandboxes, and don't break things"
slug = "2023-08-16-sandboxes" 
tags = ['leadership', 'tech']
categories = []
externalLink = ""
series = []
+++

One of the most important things you could be doing as a tech lead is making sure there are plenty of sandboxes.

This is easily overlooked. After all, you won't be shipping a sandbox to production. Sandboxes are for play, not for "real work". When time budget is tight, you cut on play and anything that is not directly relevant for delivery.

Having sandboxes however brings up one thing, which is rarely available on production projects - freedom to experiment. Try dangerous new things with zero consequences. Be bold.

Production projects are bound by constraints. We want to make sure that breaking things is difficult. This comes at cost - change while possible becomes slow, requiring consensus and lots of iterations. In a self-respecting project we'd usually limit:

* Pushing directly to main branch
* Merging pull-requests when tests are failing
* Merging PR:s when tests are missing
* Dramatic changes to infrastructure
* Changing CI/CD pipelines so they are different from the rest of the projects

All of the above makes sense. To make changes less breaking, we must pay the cost of convenience. A good project usually tends to find a delicate balance between developer experience and broken production. A bad project leans towards health metrics thinking this is the ultimate good, and developers will cope somehow.

Sandboxes could also be a cure for overly complex legacy projects, where all hope is seemingly lost, and best sailors have long abandoned the ship. A better way of convincing product management of the need to a change is to demonstrate a proof of concept. Implementing PoC:s in a sandbox environment is a breeze, a straightforward and inspiring time in a field full of green. Skip the conventions, prove the point and demonstrate the goal. This tends to get sign offs and time from the team to spend on a real implementation.

Examples of sandboxes could include:
* A Github repository with unlocked main branch and full admin access to everyone on the team. Useful when you want to try / debug Github workflows and actions.
* Sandbox Kubernetes cluster with unlocked configs, so that you could try Kubernetes features in a close to production environment - vs running things locally on minikube
* Cloud project with full access to resources. Useful when spiking new infrastructure changes, experimenting with cloud configurations and upskilling on new cloud native products.
* Sandbox budget - money for trialling new services and tools that improve developer experience and enable better delivery

Sandbox is a safe space where breaking things is the norm. RnD work of course requires capacity for failure, but in a safe way, enabling learning and quick feedback loop. Poking things and getting feedback is how engineers generally work day-to-day, except sometimes it takes ages for the feedback to propagate. And sometimes feedback would also bring down the very product we're building.

Creating sandboxes however requires a good set of privileges. Which is why this is up to a tech lead to make sure there are plenty. Depending on your project, everyone might have admin access to everything - or no one has access to anything. Tech leads usually are the ones in the middle, who tend to have just enough permissions to create new sandboxes, as well as promote their usage through example. Honestly, promotion is easy - engineers do appreciate trust and safe space, and being able to try new things without a fear of consequences is a perfect spot to be.

Having no sandboxes could mean a red flag. This usually means there is no easy way to change things in a safe way. While the delivery process might be there, full of conventions and obstacles, a larger change will require a lot of convincing, and even then obtaining commitment is a difficult task. How would you commit time and money when there's no proof of the outcome? The first thing you'd want to do is to start making a space for sandboxes.

Day-to-day work should be fun after all - and playing in a sandbox makes a happy software engineer.
