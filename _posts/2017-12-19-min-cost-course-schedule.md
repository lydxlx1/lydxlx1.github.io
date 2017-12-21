---
author: lydxlx
date: 2017-12-19
layout: post
title: "Min Cost Course Schedule"
description: ""
mathjax: true
tipue_search_active: true
categories: algorithm
tags: greedy dp reduction
---

## Problem
[LeetCode 630](https://leetcode.com/problems/course-schedule-iii/description/)的加强版，我把它称为**Min Cost Course Schedule**。  
给定$n$个course，每个course有三个属性
- 完成该课程需要的连续的时间$t_i$,
- 该课程的截止时间$d_i$,
- 修完该课程可以获得学分$c_i$.

这里不妨假设所有的数都是正整数，并且$t_i \le n$。
现在要求一种最优的选课方式，使得总学分数最多。

## Hardness Result & Solution
首先，我们证明这个问题至少和01-背包一样难。

给定一个01-背包的问题：$n$个物体，每个物体的体积是$w_i$，价值是$v_i$。背包的总体积是$W$。  
我们构造这样的一个min cost course schedule的问题实例。定义$n$个courses，每个course的完成时间记为$w_i$，获得学分数为$v_i$，所有的course的截止时间均为$W$。  
很显然，后者问题的最优解直接imply前者01-背包的一个最优解。

接着我们给出一个基于DP的伪多项式解法。  
我们先将所有的courses按照截止时间$d_i$从小到大排序，然后我们会有下面这个重要的（基于贪心的）结论。

**Lemma**
假设在某组最优解中，我们学习了课程$i_1, i_2, \dots, i_m$，这里$i_1 < i_2 < \dots < i_m$，那么也一定存在一组最优解使得我们从左到右**顺次**学习这些课程。  
**证明：** 假设结论不立，那么一定会存在$i_x$和$i_y$使得我们先上$i_x$，然后**紧接着**就上$i_y$，但是$x > y$。  
不妨假设$i_x$之前的课我们一共花了$T$的时间，于是我们一定有  
(1) $T + t_{i_x} \le d_{i_x}$,  
(2) $T + t_{i_x} + t_{i_y} \le d_{i_y}$,  
(3) $d_{i_x} \le d_{i_y}$ （这是因为$x > y$）.  
现在我们颠倒一下$i_x$和$i_y$的学习顺序得到一组新的解（即，先学$i_y$，后学$i_x$），我们证明这组解依然是合法的，所以也是一组最优解（因为学习的课程总数并没有发生变化）。  
(1) $i_y$之前和$i_x$之后的所有课程显然不会受到任何影响，所以它们一定是合法的。  
(2) 考察$i_y$，我们总共画的时间是$T + t_{i_y} \le T + t_{i_x} + t_{i_y} \ge d_{i_y}$，所以先上$i_y$没有问题。  
(3) 然后考察$i_x$，我们总共花的时间是$T + t_{i_y} + t_{i_x} = T + t_{i_x} + t_{i_y} \le d_{i_y} \le d_{i_x}$，所以再上$i_x$也是合法的。$\Box$


有了上述Lemma，我们定义DP的状态$f[i][j]$表示：给定课程0到$i$，在累计上课时间不超过$j$的情况下，我们最多可以获得的学分数。状态转移如下：  

$$
f[i][j] = \left\{
\begin{array}{cl}
0 & \mbox{if } i < 0 \mbox{ or } j \le 0 \\
f[i][d_i] & \mbox{else if } j \ge d_i \\
f[i-1][j] & \mbox{else if } j < t_i \\
\max(f[i-1][j], f[i-1][j-t_i]) & \mbox{else}
\end{array}  
\right.
$$.

正确性读者可以自行理解，其中最后一个转移式子用到了上述的Lemma，它保证了我们可以把这个课放在最后学习。最终答案是$f[n - 1][\min(\sum{t_i}, d_{n-1})]$。 时间复杂度是$O(\min(n^3, nd_{n-1}))$。

最后，上述的DP其实基本上和01-背包无异，也就是说这两个问题其实是等价的，同属于NP-Complete类。
