---
author: lydxlx
date: 2020-04-23
layout: post
title: "Numpy argmax does not populate from generator objects correctly"
description: ""
mathjax: true
tipue_search_active: true
categories: python
tags: python numpy
---

* content
{:toc}


Consider the following examples:
```python
import numpy as np

print(np.argmax([1, 2, 3, 4]))
print(np.argmax(np.array([1, 2, 3, 4])))
print("---")
print(np.argmax(range(4)))
print(np.argmax(np.array(range(4))))
print("---")
print(np.argmax(i for i in range(4)))
print(np.argmax(np.array(i for i in range(4))))
```

The output is
```
3
3
---
3
3
---
0
0
```

So it seems like for `np.argmax`
- regular list and its wrapped np array work,
- range and its wrapped np array work,
- generator object or its wrapped np array do not work.
