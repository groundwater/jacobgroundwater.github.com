---
layout: post
title: "Parametric Active Contours"
description: ""
category: Notes
tags: [math, image-processing]
---
{% include JB/setup %}

## Arrays are Functions

Image processing involves frequently going between the discrete and continuous world.
Intuition can break down without a few keystones.

Think of arrays as functions, first and foremost.
A image will be loaded as a 2D array, indexed from 0.
We will refer to the domain of pixel often, so let's call them <span>\(P\subseteq \mathbb{N}\times\mathbb{N}\)</span> where
<div>\[P=[0,n-1]\times[0,m-1]\]</div>

An <span>\(n\times m\)</span> array <span>\(A\)</span> in the discrete world
should also be recognized as a function <div>\[A:P\rightarrow [0,255]\]</div>
for 8-bit images.

We can create a continuous analogue of this function, something that agrees with <span>\(A\)</span>
for discrete values, but is continuous on the plane <span>\(P\)</span>,
and differentiable.

## Use Parametric Curves

Parametric curves are different from geometric curves.
A geometric curve is a relationship between <span>\(x\)</span> and <span>\(y\)</span>,
expressed as an implicit or explicit equation i.e.
<div>\[ x^2 + y^2 = 1\]</div>

Parametric curves on the other hand explicitly but separately give the <span>\(x\)</span> and <span>\(y\)</span> values,
with respect to a time parameter <span>\(s\)</span> that evolves from 0 to 1.
<div>\[u(s) = \left[ \begin{array}{c} sin(2\pi s) \\ cos(2\pi s) \end{array}\right]\]</div>

There are techniques for evolving both geometric and parametric curves, but they are not interchangeable.
We will be looking at parametric curves *only*.

## Create a Functional

A functional is something that assigns _weights_ or scalar values to functions.
We use functionals all the time for discrete values.
Calculating an average is a functional, where the function maps items to prices/grades/values.

To calculate functionals for continuous functions, we often use an integration over the entire function.
The <span>\(L_1\)</span> norm of <span>\(u\)</span> is a measurement using the functional 
<div>\[\int_S u(s) ds\]</div>
where the domain of <span>\(u\)</span> is <span>\(S\)</span>.

When doing image segmentation, <span>\(u\)</span> is unknown.
We must design a program to _discover_ the best possible <span>\(u\)</span> for image <span>\(I\)</span>.
We can solve for <span>\(u\)</span> if we design our functional to have _minimal energy_ when <span>\(u\)</span>
best segments our image.

## Solve with Euler-Lagrange



