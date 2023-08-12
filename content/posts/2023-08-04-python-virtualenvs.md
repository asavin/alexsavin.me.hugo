+++ 
draft = false 
date = 2023-08-04T10:37:10Z
title = "Python virtual environments howto"
description = "Python virtual environments howto"
slug = "2023-08-04-python-virtualenvs" 
tags = ['python', 'engineering']
categories = []
externalLink = ""
series = []
+++

Python is one of the most popular languages in the world - not the least thanks to its application in ever growing popularity of ML and data science. As there are a number of tools helping you with a local Python setup, I thought to share best practices and ways of dealing with things like multiple Python versions, libraries and virtual environments. All very much hands-on, and tested at the point of writing of this blog.

All sample commands are for bash / zsh on MacOS. However if you replace `brew` with `apt-get`, that might just enable Linux and WSL too.

Your scenarios will vary, so we'll start with something very basic.

Pre-requisites - you have [brew](https://brew.sh/) package manager installed and good to go.

## One version of Python ought to be enough for everyone

`brew install python` is a good start. This will give us Python, globally available too. Now we can also install libraries with `pip`: `pip install [package name]`. All packages will be available globally.

## What if I need multiple versions of Python?

A very useful and realistic scenario when you want to install and switch between multiple versions of Python. `pyenv` to the rescue.

`brew install pyenv`

Pyenv is a very powerful tool, but for now we can:
* `pyenv install --list` - list all versions of Python available for installation
* `pyenv install 3.11.1` - install Python version 3.11.1 locally
* `pyenv versions` - list all locally installed versions of Python
* `pyenv global 3.11.1` - set Python 3.11.1 as a globally available version

Now we can manage multiple versions of Python.

## I want to install Python packages in separate environments and switch between environments

Having all packages in a global scope can quickly become a problem when we're managing multiple versions of Python, and potentially dealing with multiple projects. There must be a way to have isolated environments where we could have sets of installed packages specific to a current app.

Python contains a built-in way of dealing with this. It is called `venv` - short for "virtual environment". This is how it works:

* Navigate to a folder of your project
* `python -m venv my_isolated_env` - this creates a new sub-directory named `my_isolated_env`
* `source my_isolated_env/bin/activate` - activate new virtual environment.
* `deactivate` - to drop out of the virtual environment back to the global scope.

Venv is nice, but not ideal. For example, you want a unified way to manage both Python version and a virtual environment it is attached to. Enter `pyenv-virtualenv` - a pyenv plugin that allows you to do just that.

* `brew install pyenv-virtualenv` - install the plugin
* `pyenv virtualenv 3.11.1 my-env` - create a new virtual environment based on Python 3.11.1 and named "my-env".
* `pyenv virtualenvs` - list all virtual envs you've created
* `pyenv activate my-env` - activate existing virtual environment
* `pyenv deactivate` - deactivate virtual environment and drop out to global context
* `pyenv uninstall my-env` - remove virtual environment

You can also enable automatic activation of a previously created virtual environment if you place a file named `.python-version` at the root of your project. The file should simply contain name of the virtual environment:

```
my-env
```

## Can I manage packages, Python version and virtual environment on a project level?

When working with complex projects and in a team environment, you want to share and align as much of developer setup as possible. [Poetry](https://python-poetry.org/) will help us here.

Poetry is a more formal dependency manager, much like `npm` or `yarn` in the Node world. It will create a lock file and provide a manifest of packages required by the project. It will also declare Python version requirements, and it can create virtual environments for every project.

Note that Poetry will not install Python versions - you would still need `pyenv` for that.

Poetry is incredibly powerful and flexible. You can use it in combination with `pyenv virtualenv` or even `python venv` if you choose so.

`poetry env info` is an extremely useful command when trying to double check what environment are we currently in.

## So how do you combine all of this for a real-world multi-project scenario?

Here's my setup:
* Pyenv with virtualenv plugin
* Poetry installed globally via brew
* For each project create a new virtual environment with `pyenv virtualenv` - this might require a bit of work in the beginning, but needs to be done only once per project.
* Poetry is configured to not create virtual environments, so it doesn't clash with `pyenv virtualenv`. This is achieved with `poetry config virtualenvs.create false`

