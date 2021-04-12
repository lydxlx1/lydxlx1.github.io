---
author: lydxlx
date: 2021-04-11
layout: post
title: "Union in SQL"
description: ""
mathjax: true
tipue_search_active: true
categories: sql
tags: sql union
---

* content
{:toc}

Union in SQL performs implicit deduping on all the columns, which can cause certain bugs if not paying enough attention.


For example, the output of the following SQL will only return ONE row.

```sql
SELECT
  key
FROM (
  SELECT
    1 AS key

  UNION ALL

  SELECT
    1 AS key

  UNION ALL

  SELECT
    1 AS key

)

UNION

SELECT
  key
FROM (
  SELECT
    1 AS key

  UNION ALL

  SELECT
    1 AS key

  UNION ALL

  SELECT
    1 AS key

)
```

If we are using `UNION ALL` instead, the result will contain 6 rows instead.

