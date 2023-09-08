+++ 
draft = false 
date = 2023-09-08T10:37:10Z
title = "Github Workflows and multilines in YAML"
description = "YAML, lots of YAML"
slug = "2023-09-08-github-workflows" 
tags = ['cicd', 'github', 'workflows']
categories = []
externalLink = ""
series = []
+++

Github Actions are gaining more popularity, thanks to them being right next door to your repository. Lately I've noticed Github also actively suggesting workflow templates based on the contents of your repo, like "hey, I see you've got a NodeJS project going, how about we build it here too?". It's not a bad options, and my biggest complaint so far is about YAML - like with any other YAML driven project it's fine in the beginning, but becomes this unwieldy monstrosity once you require any degree of advanced complexity to fit the needs of your project.

And here's something that YAML is especially not good at - multilines.

## Multilines

Workflows are stored in yaml files, and yaml is very sensitive to both line breaks and indentations. This means a massive pain when you do need to add some multiline content.

## Interpolation of step results

Workflows allow you to define multiple steps, and use results of previous steps in the latter ones. The way this works though is quite interesting - GH action runner would literally interpolate contents of the result into the code of the step, and then attempt to run it. This easily results in broken step code - especially if the interpolated contents is multilined.

Example - we want to use a previous step output in a JavaScript code.

```yaml
name: "My multiline pain"

on:
  workflow_call:

jobs:
  my-multiline-job:
    runs-on: ubuntu-latest
    steps:
      - name: "Multiline step output"
        id: multiline-output
        ... // output to a variable "list"
      - uses: actions/github-script
        id: js-step
        with:
          result-encoding: string
          retries: 3
          retry-exempt-status-codes: 400,401
          script: |
            const multilineResult = `${{ steps.multiline-output.outputs.list }}`

```

After interpolation our script will become something like:

```yaml
script: |
  const multilineResult = `line1
  line2
  line3`
```

...which is still a valid JavaScript. Backtick string wrapper is very useful for our goal. Unlike single tick or double tick, in JavaScript backtick supports multiline.

This works great - that is until your interpolated string would also contain a backtick. At this point your JS code will become faulty and the step will fail.

One way to solve the backtick multiline string issue that I can think of would be pre-processing the string in a separate step and replace all backticks with a special sequence of characters.  `sed` bash command could achieve that - here we'll replace all backticks with triple stars:

```bash
sed 's/`/***/g'
```

Later, in JavaScript code, once interpolation is done, we can find and replace that special sequence into backtick characters.

```js
const multilineResult = `${{ steps.multiline-output.outputs.list }}`
strWithBackticks = str.replace(/\*\*\*/g, "`");
```

Either way, writing Github workflows requires a good amount of creative thinking.

## A multitude of syntaxes

A given workflow while natively yaml could contain following syntaxes under the same roof:
- Bash scripts
- JavaScripts
- Python scripts

All intermixed with Github context variables and YAML itself. This can be a recipe for disaster, and  most code editors will struggle to correctly parse such workflows. This means operating almost blindly - doubly so since you cannot test your changes locally. The only way to validate a workflow is to push it to Github and trigger a run.

## Sandbox repository

When operating on a production codebase, I would strongly recommend not to tweak workflows in-place. Chances are, your workflows are responsible for building and deployment process - which is something you don't want to break.

Instead I've ended up making a sandbox repository, mostly replicating the structure of a production repo, with files and necessary artifacts in place. This way I could push my (sometimes radical) changes to Github, trigger workflow run, and verify that things are behaving the way they suppose to. With complex enough workflows lots of things could go wrong - and running this first on a sandbox repo was a massive save.

## IDE support

Github workflows are YAML files, and hence you get YAML syntax highlighting in most editors, and not much else. The only notable exception was VSCode. When connected to the GH organisation and with access to our private repositories, it was able to resolve re-usable workflows - and validate provided inputs - or highlight the lack of those. If you are planning to spend a lot of time building release pipelines on Github, I would heavily recommend switching to VSCode for that work.

## Re-usable workflows

You can extrapolate parts of your workflows and make them re-usable. This will require making a new repo, and in the past Github required you to have that repo public. But not anymore - you can have a private repo with re-usable workflows, and have them re-used within your org.

## Forward thinking

Could we have a CI that wouldn't use YAML? A JS / Python drive CI system would be a massive step forward for us all.
