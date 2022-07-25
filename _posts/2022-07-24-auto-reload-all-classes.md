---
author: lydxlx
date: 2022-07-24
layout: post
title: "How to auto-reload all the modules and classes in Python Notebook?"
description: ""
mathjax: true
tipue_search_active: true
categories: css
tags: python notebook autoreload
---

* content
{:toc}

The answer is `autoreload`. See the following Line Magics.
```python
In [1]: %load_ext autoreload

In [2]: %autoreload 2

In [3]: from foo import some_function

In [4]: some_function()
Out[4]: 42

In [5]: # open foo.py in an editor and change some_function to return 43

In [6]: some_function()
Out[6]: 43
```

This [official page](https://ipython.org/ipython-doc/3/config/extensions/autoreload.html) contains more details on `autoreload`.

