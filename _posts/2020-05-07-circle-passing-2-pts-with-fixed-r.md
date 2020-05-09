---
author: lydxlx
date: 2020-05-07
layout: post
title: "Center of the circle passing through two points with fixed radius"
description: ""
mathjax: true
tipue_search_active: true
categories: math geometry
tags: computational-geometry circle template algorithm
---

* content
{:toc}


## The Question
Given two different points $$P = (x_1, x_2)$$ and $$Q = (y_1, y_2)$$ and a real number $r$,
we want to compute the center of circle that pass through both points with radius $r$.
It is easy to verify that there is/are (i) no solution if $r < \overline{PQ}$, (ii) exactly one solution
if $r = \overline{PQ}$, and (iii) two solutions if $r > \overline{PQ}$, where
$\overline{PQ}$ denotes the $L_2$ distance from $P$ to $Q$.

{:refdef: style="text-align: center;"}
![](/images/2020-05-07.svg){:height="200px"}
{:refdef}

## Step 1
Find the direction that is perpendicular to $\overrightarrow{PQ} = (x_2 - x_1, y_2-y_1)$.
A simple solution is $\overrightarrow{d} = (y_1-y_2,x_2-x_1)$, where $\overrightarrow{d}$ and $\overrightarrow{PQ}$ has the same norm.
Let's denote the norm $\sqrt{(x_1-x_2)^2+(y_1-y_2)^2}$ by $p$, and thus $\overrightarrow{d} / p$ will be a unit vector.
For convenience, we redefine the symbol $\overrightarrow{d}$ to represent that unit vector.

## Step 2
Compute the midpoint $M$ of $P$ and $Q$, where $M = ((x_1+x_2)/2, (y_1+y_2)/2)$.
Now, we just need to start from $M$ and move along the direction or the opposite direction of $\overrightarrow{d}$ by $\lambda$,
where $\lambda = \sqrt{r^2 - (p/2)^2}$. That is, the circle center $C$ is equal to

$$
C = M \pm \lambda\overrightarrow{d}.
$$

## Python Code
```python
def centers(x1, y1, x2, y2, r):
    q = ((x2 - x1) ** 2 + (y2 - y1) ** 2) ** 0.5
    x3 = (x1 + x2) / 2
    y3 = (y1 + y2) / 2

    xx = (r ** 2 - (q / 2) ** 2) ** 0.5 * (y1 - y2) / q
    yy = (r ** 2 - (q / 2) ** 2) ** 0.5 * (x2 - x1) / q
    return ((x3 + xx, y3 + yy), (x2 - xx, y3 - yy))
```
