---
author: lydxlx
date: 2020-03-08
layout: post
title: "LeetCode Weekly Contest 178"
description: ""
mathjax: true
tipue_search_active: true
categories: coding
tags: leetcode
---

* content
{:toc}

## 1365. How Many Numbers Are Smaller Than the Current Number
[[Problem](https://leetcode.com/problems/how-many-numbers-are-smaller-than-the-current-number/)]
[[Code](https://github.com/lydxlx1/LeetCode/blob/master/src/how-many-numbers-are-smaller-than-the-current-number.py)]

Since each number is within the range [0, 100], we can use a counting sort based approach.
1. Do a linear-time counting.
2. Compute the prefix sum.
3. Answer each query in O(1) time.

Time: $$O(n)$$  
Space: $$O(100)$$  

## 1366. Rank Teams by Votes
[[Problem](https://leetcode.com/contest/weekly-contest-178/problems/rank-teams-by-votes/)]
[[Code](https://github.com/lydxlx1/LeetCode/blob/master/src/rank-teams-by-votes.py)]

Assume there are m rounds of voting, we can solve this problem by a radix sort (from the m-th round to the first round).

Time: $$O(m * (26 \log 26))$$, which can be further optimized to $$O(26m)$$ using counting sort.  
Space: $$O(26)$$  

## 1367. Linked List in Binary Tree
[[Problem](https://leetcode.com/problems/linked-list-in-binary-tree/)]
[[Code](https://github.com/lydxlx1/LeetCode/blob/master/src/linked-list-in-binary-tree.py)]

It is hard to solve the problem in a top-down fashion since each tree node can have two choices.
However, since each node has a unique parent, the upwards paths ending at any node are also unique (by its length).
This suggests a DFS approach, where we just need to check whether the last m nodes on the stack match the given listed list at any time.

Time: $$O(mn)$$  
Space: $$O(m + h)$$  
m = linked list size, n = binary tree size, h = binary tree height

## 1368. Minimum Cost to Make at Least One Valid Path in a Grid
[[Problem](https://leetcode.com/problems/minimum-cost-to-make-at-least-one-valid-path-in-a-grid/)]
[[Code](https://github.com/lydxlx1/LeetCode/blob/master/src/minimum-cost-to-make-at-least-one-valid-path-in-a-grid.py)]

This is a single source shortest path problem.

Build the graph
- For each grid cell, create four directed edges to its neighbors (if exist).
- The weight of the edge is 0 if the edge direction matches with the number in cell, otherwise the weight is 1.
  This means each cell will have exactly one outgoing edge with 0 weight, and two or three outgoing edges with weight equal to 1.o
- Then, the length of the shortest path from top-left to bottom-right will be the answer.

Time: $$O(mn \log (mn))$$, which can be further optimized to $$O(mn)$$.
      This is because weights of edges in this graph are either 0 or 1, so we can compute the shortest path using BFS with a Deque.
      Formally, we insert to the head of the queue if the edge weight is 0 and insert to the tail of the queue if weight is 1.  
Space: $$O(mn)$$
