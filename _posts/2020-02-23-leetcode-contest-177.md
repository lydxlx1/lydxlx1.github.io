---
author: lydxlx
date: 2020-02-23
layout: post
title: "LeetCode Weekly Contest 177"
description: ""
mathjax: true
tipue_search_active: true
categories: coding
tags: leetcode
---

* content
{:toc}

## 1360. Number of Days Between Two Dates
[[Problem](https://leetcode.com/problems/number-of-days-between-two-dates/)]
[[Code](https://github.com/lydxlx1/LeetCode/blob/master/src/number-of-days-between-two-dates.py)]

Most programming languages should have date related packages. Worth getting familiar with them.

## 1361. Validate Binary Tree Nodes
[[Problem](https://leetcode.com/problems/validate-binary-tree-nodes/)]
[[Code](https://github.com/lydxlx1/LeetCode/blob/master/src/validate-binary-tree-nodes.py)]

There are multiple ways to validate a binary tree. Here is one way of doing that.
- There must be exactly $n - 1$ edges.
- There must be exactly one node with 0 in-degree, and that node is the root.
- Every other node must have in-degree equal to one.

Time: $$O(n)$$
Space: $$O(n)$$

## 1362. Closest Divisors
[[Problem](https://leetcode.com/problems/closest-divisors/)]
[[Code](https://github.com/lydxlx1/LeetCode/blob/master/src/closest-divisors.py)]

There can be at most $$\sqrt(n)$$ pairs of divisors, so we can just enumerate all of them.

Time: $$O(\sqrt(n))$$
Space: $$O(\sqrt(n))$$, which can be further optimized to $O(1)$.

## 1363. Largest Multiple of Three
[[Problem](https://leetcode.com/problems/largest-multiple-of-three/)]
[[Code](https://github.com/lydxlx1/LeetCode/blob/master/src/largest-multiple-of-three.py)]

This is a math problem. We first have two facts that are easy to verify.
1. Since $$10^x \mod 3 = 1 (x \ge 0)$$, a number is a multiple of three if and only if the sum of digits is a multiple of three.
2. When the set of digits is given, to gain the max value, we should concatenate them in decreasing order.
   And if the largest digit is zero (no matter how many zeros are there), the answer is also zero.
   If the set of digit is empty, we output empty string.
   
Then, it is easier to solve this problem backwards, i.e.,
considering the digits we have to discard to make the final number as large as possible.
Sum up all the digits and we have three cases based on its modulo (by 3).
1. mod = 0. This is a happy case, and we should just use up all the digits.
2. mod = 1. We should either discard a digit (that is 1 mod 3) or discard two digits (that are both 2 mod 3).
   Prefer to discard fewer digits.
3. mod = 2. We should either discard a digit (that is 2 mod 2) or discard two digits (that are both 1 mod 3).
    Again, prefer to discard fewer digits.

Time: $O(n log n)$, which can be optimized to $O(n)$ using counting sort.
Space: $O(n)$
