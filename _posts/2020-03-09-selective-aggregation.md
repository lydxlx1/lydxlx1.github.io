---
author: lydxlx
date: 2020-03-09
layout: post
title: "Selective Aggregation (in Presto)"
description: ""
mathjax: true
tipue_search_active: true
categories: sql
tags: sql presto 
---

* content
{:toc}

When counting in aggregation, you are probably familiar with both `COUNT()` and `COUNT_IF()`,
where the latter counts after a selective filter.
However, when it comes to other aggregation functions, there are simply no the corresponding `_IF` versions.
One could argue that we could put the filter in `WHERE`,
but this will not scale if we want to do multiple selective aggregations.
Consider the following examples.
It would be really convenient to have these `_IF` aggregation variants,
and otherwise one has to do each selective aggregation separately and finally join them together.

```sql
SELECT
  key,
  SUM_IF(val1, condition1) AS sum1,
  SUM_IF(val1, condition2) AS sum2,
  ARRAY_AGG_IF(val2, condition3) AS vals,
  ...
FROM
  table
GROUP BY
  1
```

## Solution - Selective Aggregation
We can now write the following query in Presto for selective aggregations.

```sql
SELECT
  key,
  AGG1(x) FILTER (WHERE condition1),
  AGG2(y) FILTER (WHERE condition2),
  AGG3(z) FILTER (WHERE condition3),
  ...
FROM
  table
GROUP BY 
  1
```

## Fun Fact
I only surfaced this cool feature from [this request](https://github.com/prestodb/presto/issues/5085) on Presto's Github page.

As stated by the last comment,
> Is this feature documented anywhere? I only found it because https://stackoverflow.com/questions/55504820/presto-filter-array-of-rows-inside-aggregation

As of now, I still cannot find any related document on Presto's main page, and this feature has just been silently supported since Dec 20, 2016...
