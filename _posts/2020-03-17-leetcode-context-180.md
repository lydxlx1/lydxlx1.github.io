---
author: lydxlx
date: 2020-03-17
layout: post
title: "LeetCode Weekly Contest 180"
description: ""
mathjax: true
tipue_search_active: true
categories: coding
tags: leetcode
---

* content
{:toc}

## 1380. Lucky Numbers in a Matrix
[[Problem](https://leetcode.com/contest/weekly-contest-180/problems/lucky-numbers-in-a-matrix/)]
[[Code](https://github.com/lydxlx1/LeetCode/blob/master/src/lucky-numbers-in-a-matrix.py)]

Since all elements are distinct in the matrix, we can pre-compute the min value per each row and the max value per each column.
Then, we scan the matrix one more time and find all the candidates.

Time: O(mn)  
Space: O(m + n)

## 1381. Design a Stack With Increment Operation
[[Problem](https://leetcode.com/contest/weekly-contest-180/problems/design-a-stack-with-increment-operation/)]
[[Code](https://github.com/lydxlx1/LeetCode/blob/master/src/design-a-stack-with-increment-operation.py)]

Maintain each prefix increment pointwisely and lazily. 
Then all operations can be implemented in O(1) time.

## 1382. Balance a Binary Search Tree
[[Problem](https://leetcode.com/contest/weekly-contest-180/problems/balance-a-binary-search-tree/)]
[[Code](https://github.com/lydxlx1/LeetCode/blob/master/src/balance-a-binary-search-tree.py)]

Do an in-order traversal to obtain all the elements in BST in sorted order.
Then build the balanced tree using Divide-and-Conquer.

Time: O(n)  
Space: O(n)

## 1383. Maximum Performance of a Team
[[Problem](https://leetcode.com/contest/weekly-contest-180/problems/maximum-performance-of-a-team/)]
[[Code](https://github.com/lydxlx1/LeetCode/blob/master/src/maximum-performance-of-a-team.py)]

Enumerate the engineer that has the minimum efficiency in the team.
When each engineer is fixed, find those (at most) k engineers that have top speed.
This algorithm can be implemented efficiently by (i) a pre-sorting on efficiency in decreasing order and (ii) using a heap or BST to maintain top-k speed.

Time: O(n log n + n log k) = O(n log n)  
Space: O(k + sorting). When using (say) heap-sort, the complexity becomes O(k).
