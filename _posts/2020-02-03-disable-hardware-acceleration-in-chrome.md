---
author: lydxlx
date: 2020-02-03
layout: post
title: "Disable hardware acceleration in Chrome"
description: ""
mathjax: true
tipue_search_active: true
categories: english
tags: chrome wechat
---

* content
{:toc}

## 背景
自从更新了新的macOS到Catalina，我陆陆续续发现了一些问题。
- 微信和其他窗口之间切换一直特别卡，会有1-2秒左右的延迟。
- Google Keep在chrome里切换tab也会特别卡，但是在其他浏览器（Firefox, Safari, ...）中却没有这样的问题。

很长一段时间，我一直把锅丢给Chrome和mac的新操作系统...

## 解决方法
也许是歪打正着，我今天的chrome特别卡，吃了所有的cpu，于是便在网上搜一搜有没有好的解决方法。之后发现了一个帖子说禁用 **Use hardware acceleration when available** 这个选项会有一定的效果。
禁用了以后并没有显著改善chrome吃cpu的问题，但是发现微信以及Google Keep现在都可以瞬时切换了！建议遇到过类似问题的小伙伴也试试看，希望也可以解决你们的问题！

## 一个小发现
看来mac版本的微信内部是用Chrome来渲染的。
