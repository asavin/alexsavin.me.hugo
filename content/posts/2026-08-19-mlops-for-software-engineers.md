+++ 
draft = false 
date = 2026-08-19T01:37:10Z
title = "MLOps for software engineers - Part 1: What is an ML model?"
description = "Intro to MLOps for software engineers, and models as pure functions"
slug = "2026-08-19-mlops-for-software-engineers" 
tags = ['mlops']
categories = []
externalLink = ""
series = []
+++

I'm not an MLOps engineer. However for the past couple of years I've been working side-by-side with data scientists to create, deploy and monitor bespoke ML models. This blog is for software engineers, who might find themselves in a similar scenario.

This is especially likely if your title contains anything "full-stack" - these days this would definitely include some degree of MLOps, if your product is employing any level of modelling or prediction.

There is a lot of mystery and black boxes when it comes to ML, and I hope to disperse some of that fog. After all, we're all engineers, and this is very much an engineering domain. We will not be covering the actual data science behind the modelling techniques. Although, if it comes to that, I'd be happy to dip a toe. _That_ domain is largely advanced math, which is a special kind of fun that software engineers rarely get to enjoy.

## ML model as a pure function

Any fans of functional programming here? Good.

Think of a model as a pure function.

![](https://alexsavin.me/photos/2026-08-19-mlops-for-software-engineers/model-as-pure-function.png)

There are inputs with a pre-defined schema. There are outputs, also in a pre-defined format. The model takes inputs, and produces outputs. A pure function.

Let's say our model is going to predict an outcome of dividing input by 2.

![](https://alexsavin.me/photos/2026-08-19-mlops-for-software-engineers/model-input-output.png)

Now we have an input of a shape `{ input: number }` and an output of a similar shape `{ output: number }`.

Goes without saying, that input / output schema can be anything that the product needs.

A model could literally be a function written in any language - but most likely Python. And deep down it usually is. That function would be wrapped into a framework that would allow a model to be trained and to predict. But fundamentally this could come down to a single pure function that takes some inputs, and returns a result in a rigid, pre-defined format.

If models are just pure functions, why everything is so complex when it comes to MLOps?

## A lifecycle of a model

![](https://alexsavin.me/photos/2026-08-19-mlops-for-software-engineers/model-lifecycle.png)

Models are meant to predict what is going to happen. Traditionally we use historical data and advanced statistical math to achieve this.

When approaching a new model, the I/O and its format is really what this is all about. What is the desired output? What are the available inputs? Can we draw enough correlations between I and O to have a statistically meaningful prediction?

Both input and output data schemas are our **I/O data manifests**. Setting them in stone is very important, as it enables us to start working on model deployment, data pipelines and anything else that needs for model integration.

It is also not always possible - at least not for inputs. The output can be quite minimalistic and immutable in terms of data shape. The inputs would often have a few iterations on what is feasible to supply to the model.

A model must be _trained_. To do that you have to have a training dataset. This dataset must be sourced, sanitized, transformed and versioned. The last bit is important, as for every model iteration you want to have an easy way to refer to a particular version of a dataset.

You'd also want to version the trained models. This is different from versioning a piece of code on `git`, since the "trained" part of the model will be binary. Those are effectively the **weights** of the model - the holy grail, the most precious part that takes lots of time, effort and money to create.

Once trained, a model is deployed for _inference_. Training and inference are two fundamental modes of operation for models, and you will hear about them a lot. Same model will have different challenges when in training vs inference. Solving those challenges is what MLOps is all about.

## How this differs from software engineering

As engineers we are used to building and shipping functionality. When talking MLOps the challenges are more logistical in nature.

We need a reliable way of navigating the model lifecycle path while having a way to observe it, draw conclusions on the efficiency of a model. All parts of the process must be deterministic in nature - as in we should be able to repeat them in the future and gain the exact same artifact. While model outputs can vary for the same inputs with large complex models, training a model with a versioned dataset should always produce the same model.

## Next time

Models as artifacts?
