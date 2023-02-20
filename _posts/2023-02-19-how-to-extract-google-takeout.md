---
author: lydxlx
date: 2023-02-19
layout: post
title: "How to merge and extract tgz files from Google Takeout?"
description: ""
mathjax: true
tipue_search_active: true
categories: css
tags: tgz google takeout
---

* content
{:toc}

Source: [](https://gist.github.com/chabala/22ed01d7acf9ee0de9e3d867133f83fb)

One solution that works for me on Mac:
```bash
pv takeout-* | gtar -xzif -
```

Where we need to install `pv` and `gnu-tar` from Homebrew, i.e.,
```bash
brew install pv
brew install gnu-tar
```







