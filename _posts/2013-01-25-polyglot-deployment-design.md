---
layout: post
title: "Continuous By Design"
description: ""
category: 
tags: []
---
{% include JB/setup %}

I believe **continuous deployment** is fast becoming the standard expectation for new projects.
In order to avoid confusion, I will define what I mean more precisely.
A continuous deployment is one that:

1. is fully automated, and can be triggered by a single command
2. if the build passes, it is reasonable to expect the deployment will not break the site
3. takes under 20 minutes
4. is run daily, or multiple times per day

This is my minimum expectation of a continuous deployment system.
There are more goodies that can be added, but for the purposes of this article the above is sufficient.

# Continuous By Design

Continuous deployments impose restrictions on application design.
I would argue that many of these restrictions actually _improve_ application design.

I would like to share the concept of an **Application Bundle**, **Application Container**, and **Application Network** that I use for deployment.
Each component fits together cleanly, giving you a great deal of flexibility and control over your product.

![Bundle Design](/images/app-bundle.png)

## Application Bundle

An application bundle can be _any_ server application that adheres to the minimal interface described below.
All application bundles must have:

1. A `Procfile` used to start processes

Application may _optionally_ have:

1. A `Taskfile` used to configure, compile, and ready the application

_That's it!_

There are no language specifics to an Application Bundle,
and no constraints on project layout.
There are ways to make your application a more robust bundle however.
A robust bundle should:

1. accept external dependencies as URLs, passed in via the environment
2. start provided services via a socket, bound to either a port number from the environment,
    or a pre-opened socket provided by the boot service
3. support horizontal scaling by keeping each process stateless

## Application Container

The Application Container takes Bundles and runs the processes defined in their Procfile.
Any application that adheres to the Bundle format can be run by the container.

The container is responsible for:

1. starting each applications processes listed in the Procfile
2. logging each processes `stdout` to a central server, or local file
3. horizontally scaling the application on demand
4. restarting processes on failure, and notifying a central logger of the failure
5. deriving external dependencies

The goal of the Bundle design is to allow identical bundles to be deployed
in multiple independent **Application Networks**.

## Application Network

An Application Network is any group of containers whose bundles are interdependent.
The network can include non-bundle resources, such as databases, email, and directory services.
Generally the Network is your whole product;
in the cloud you may have one network per region, continent or zone.
Integration tests and staging environments may provide their own Network,
equal to but separate from production.

The Application Networks main job is to maintain a configuration that can be passed to its containers.

# Results

The result of the Bundle design is that running bundles are stateless, and pluggable.
Your application is now a tool that can be re-used in different situations.
Your application can be bundled as a working virtual machine image,
and deployed to test, staging, production, and different regions without needing to alter the image.

1. updating an application becomes an atomic operation
2. rolling forward or back can be achieved though re-pointing a load-balancer
3. easy fast A/B testing
4. graduated rollouts

I would argue that the restrictions imposed by the deployment will greatly improve application design.













