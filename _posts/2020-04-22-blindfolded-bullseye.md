---
author: lydxlx
date: 2020-04-22
layout: post
title: "Google Code Jam Round 1B 2020: Blindfolded Bullseye"
description: ""
mathjax: true
tipue_search_active: true
categories: math geometry algorithm
tags: code-jam binary-search interactive-problem geometry
---

* content
{:toc}

## Problem
A disc is completely contained inside a $$2\times 10^9$$ by $$2\times 10^9$$ square.
The disc radius is sufficiently large that is at least $$\frac{10^9}{2}$$,
and the disc center is always located at integer grid point.
Our job is locate the disc center using no more than 300 queries.
For each query, the system will return one of three outputs: (i) hit the center, (ii) inside the disc (but not hit the center), and (iii) outside disc.
Also note that one can only query integer grid points.

Original problem description can be found [here](https://codingcompetitions.withgoogle.com/codejam/round/000000000019fef2/00000000002d5b63).


## Solution
We can uniquely determine a circle by any three different points on its boundary; see [here](https://lydxlx1.github.io/blog/2020/04/22/circle-passing-3-pts/) on how to code the algorithm elegantly.
Given two points that are inside and outside the disc, the segment connecting them must intersect the disc boundary exactly once,
and the intersection point can then be found by binary search.
(We can maintain the invariant that one end is always inside the disc and the other end is always outside the disc.)
Once we identify three different points on the boundary, we can calculate the center although the calculation is not so trivial:

- A caveat here is that the binary search may end up with a minimal segment that contains the intersection since we are only allowed to query integer points. This is not so bad as long as the segment is short enough. One idea here is to use all $$2^3 = 8$$ possible segment endpoint combinations to approximately bound the locus of the true circle center.
- To further reduce precision errors, we can scatter the three points (segments) as much as possible.

The only problem left is how to find these points that are inside/outside the disc.
One easy solution is to find a random point that is inside the disc first.
Since the disc is completely contained inside the square, all square corners must not be contained in the disc.
We can therefore connect the random point in the disc with any three of the four square corners, form three different intersections.
The fact that square corners are far away from each other also makes the intersections well scattered.

Finally, since the disc radius is sufficiently large, we can generally find a grid point contained inside the disc by only a few random guesses.
Indeed, the expected number of attempts is no less than $$(2 \times 10^9)^2 / [\pi (\frac{10^9}{2})^2] \approx 5.1$$.

[[Python code](https://github.com/lydxlx1/cnmb1/blob/master/src/Blindfolded_Bullseye.py)]
