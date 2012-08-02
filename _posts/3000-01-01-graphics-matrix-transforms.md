---
layout: post
title: "iOS Core Animation - Matrix Transforms"
description: ""
category: Journal
tags: [ios, development, core-animation, graphics]
---
{% include JB/setup %}

The iOS Core animation framework makes heavy use of `CATransform3D` structs,
a lightweight data structure that can be manipulated to visually transform
iOS graphics layers.

The transform at its core is a 3D transformation matrix
<div>\[\left[\begin{array}{cccc}
s_x   &amp; \cdot &amp; \cdot &amp; t_x \\
\cdot &amp; s_y   &amp; \cdot &amp; t_y \\
\cdot &amp; \cdot &amp; s_z   &amp; t_z \\
\cdot &amp; \cdot &amp; \cdot &amp; h
\end{array}\right]\]</div>

Where <span>\(s_i\)</span> represents a scaling in the dimension <span>\(i\)</span>,
and <span>\(t_i\)</span> is a translation.

## Updating Transforms

I suggest creating settable properties

    @property (nonatomic,readwrite) CGFloat scale;
    @property (nonatomic,readwrite) CGFloat rotation;

and a method that calculates and updates the matrix
  
    -(void)updateLayerTransform;

Animations can merely wrap the update method

    [UIView animateWithDuration:4 animations:^{
        [self updateLayerTransform];
    }];

