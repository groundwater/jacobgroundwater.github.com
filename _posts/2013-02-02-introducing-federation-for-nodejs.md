---
layout: post
title: "Introducing Federation for Node.js"
description: ""
category: Project
tags: [nodejs,akka,actor,erlang,distributed]
---
{% include JB/setup %}

My latest project is called **Federation**,
a federated event emitter.

- [Project Homepage][3]
- [Github][4]

## Goals

1. zero setup for basic needs — federation should work out of the box
2. separation of concerns — let the sysadmins handle the wiring
3. nice API — using federation should be intuitive
4. extensible — it should be open for extension without modification (borrowed from [open closed principle][1])
5. reliable — failures are _okay_ but must be identifiable, back-pressure should prevent any cascading failures

## About

Federation borrows some terminology form the **actor model** popularized by Erlang, and now [Akka][2].
It is not a 100% faithful reconstruction of either model.
Actors are just a convenient and familiar entity, which helps with goal #3.

The key concept behind Federation is that _every_ actor has a name.
You can name your actors anything you like, there are no practical restrictions.
The name has nothing to do with _where_ the actor lives, what process it's in, or which host.
There isn't even a requirement for names to be unique, but unique names help.

Since every actor has a name, every actor can be messaged at that name.
Federation takes care of everything else.
In the following example `bob` can message the actor named `tom` with the following:

    bob.tell('tom','Hello');

It does not matter if `tom` is running within the same process, or even same host.
Actors be moved around between hosts, and their names can remain the same.
This separates the concerns of process-wiring from application logic.

Check out the [Project Homepage][3] or [Github Project][4] for more.

[1]: http://en.wikipedia.org/wiki/Open/closed_principle
[2]: http://akka.io/
[3]: http://underflow.ca/federation/
[4]: https://github.com/jacobgroundwater/federation
