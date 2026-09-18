+++ 
draft = false 
date = 2026-08-26T01:37:10Z
title = "MLOps for software engineers - Part 2: Models as Artifacts"
description = "Intro to MLOps for software engineers, training and deploying ML models to live"
slug = "2026-08-27-models-as-artifacts" 
tags = ['mlops']
categories = []
externalLink = ""
series = []
+++

How does a model becomes something that we could deploy to live?

We've established that a model itself could be considered a pure function. You supply a set of inputs, based on which a model will produce a set of outputs that would represent a prediction of a real world outcome.

One important part of this function is going to be a set of pre-defined weights. Consider this a constant value, but a quite complex one.

![](https://alexsavin.me/photos/2026-08-27-models-as-artifacts/inputs-with-weights.png)

It is created as part of model training, and then used during inference in production.

Let's talk about training.

## Training

This part will be familiar to software engineers - if you only need to do something once, you could do this easily on a local machine, running a one-off script or a tool, or a quick and dirty code that would never have to be committed.

It's only when you need something reliably repeatable, this is where you need good engineering.

This is often a problem in data science - a lot can be done in a locally run Python notebook. While you could sort of save those notebooks and re-use in the future, they are really not meant for that.

To train a model you need a dataset. The datasets are rarely available in ready-to-use shape - you'd almost always have to create one yourself.

<img src="https://alexsavin.me/photos/2026-08-27-models-as-artifacts/training-dataset-pipeline.png" class="narrow">

Assuming you have access to some kind of raw data, it would need to be transformed, mapped and reduced into a desired format of data for training. Also sanitised. We want a nice training dataset, full of nurture.

Because we want repeatability, we'd have to store and version:

- Raw data
- Transforms - often code or bash scripts, or a combo of both
- Final training dataset

This should be enough for us to repeat training at any given point.

The part about sourcing training data is probably the most critical one. If you and no one else have access to a unique dataset, however raw that might be - you are in a position to create a bespoke model, however niche that might be. This is how you start profitable companies today. Here's one example - [Verisk](https://docs.risksolutions.verisk.com/ModelDescriptions/wf-us-climateChange/climate-projections_us-wf/climate-projections-us-wf_intro_catastrophe-models.html) and their climate prediction models based on 10 000 years of weather data.

Data is truly the new oil.

Once you have the training dataset, it is time to talk about MLFlow.

## MLFlow

You need a toolset for training models, versioning models and datasets, as well as packing and serving models. [MLFlow](https://mlflow.org/classical-ml/) is that toolset today.

Once trained you want to know if this model is actually better than the previous version. This stage is called _eval_, and it is a crucial one - progress is not guaranteed, and regressions could easily happen. This is why you want to preserve all the versions of trained models - for ease of rollback, and also to compare the model performance. MLFlow will also provide us with _Model Registry_ - a way to track a 100 different experiments to see which resulting model performed the best.

<img src="https://alexsavin.me/photos/2026-08-27-models-as-artifacts/training-pickle.png" class="narrow">

Training with MLFlow will produce a _pickle_ - a binary file containing learned weights. Once combined with the model itself, you are ready to predict.

Well, sort of - you still need to package a model into something presentable. 2 popular options are - a library, or a RESTful microservice.

<img src="https://alexsavin.me/photos/2026-08-27-models-as-artifacts/model-as-rest.png" class="narrow">

MLFlow can build you this RESTful microservice out of a trained model, package that into a Docker image, ready to be served in your Kubernetes cluster. From the outside it will be a normal web service - to get a prediction you'd make a `POST /predict` or a `POST /invocations` request.

## Packaging

Once the model is baked into a RESTful service, we can also bake that into a Docker image, push it to a registry and make it deployable as a standalone instance, or to a Kubernetes cluster. This Docker image would be fully self contained, with a model, trained weights and endpoints available to be invoked.

From the outside this might look just like another service in the system.

## Next time

What if our model is hungry for more data?
