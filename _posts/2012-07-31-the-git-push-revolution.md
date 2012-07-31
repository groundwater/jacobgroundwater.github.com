---
layout: post
title: "The Git Push Revolution"
description: ""
category: Editorial
tags: [git, development]
---
{% include JB/setup %}

Everyone seems to know that Git is distributed, 
but what most people do not realize is that git is peer-to-peer.
A git repository can setup any number of **remotes** as necessary.

Using `git clone <source>` will automatically setup a remote called `origin`
which points to the source repo.

Many companies, such as [Heroku](http://www.heroku.com/) and [Github](http://github.com) now _deploy_ code via a Git remote.
By setting up the appropriate remote, developers can deploy a new build with
nothing more than `git push heroku master`, or `git push github master`.

[Github pages](http://pages.github.com/) are deployed this way, along with all [Heroku](http://www.heroku.com/) applications.

Automated testing can be done the same way,
where developers push their branch to a test server e.g. `git push jenkins mybranch`.

This is the _Git Push Revolution_.

Anybody can setup this same strategy using [Git hooks](http://git-scm.com/book/en/Customizing-Git-Git-Hooks).