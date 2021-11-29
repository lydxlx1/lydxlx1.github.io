---
author: lydxlx
date: 2021-11-28
layout: post
title: "How to hide WPM box in Typeracer?"
description: ""
mathjax: true
tipue_search_active: true
categories: css
tags: typeracer wpm css
---

* content
{:toc}

[Typeracer](https://play.typeracer.com/) is one of my favorite typing website, and I have used the "Practice Yourself" feature a lot to improve my typing accuracy and speed (and also for fun!).

Recently, I have been thinking whether it's possible to **hide the WPM (words per minute) box** while typing so that I will get less distracted by the real-time WPM number and thus can focus more on the typing paragraph.

![](/images/2021-11-28.png)

I posted the question in the Typeracer Discord channel, and [KeeganT](https://data.typeracer.com/pit/profile?user=keegant) proposed a very neat solution using CSS. 

```css
.rankPanel {
    display: none;
}
```

To enable it, one can follow these steps, assuming using Chrome as the browser.
- Open "Inspect" tool
- Go to "Sources" tab
- Locate the website's CSS file. As of now, it's named as `TypeRacer.css`.
- Append the above code snippet at the end of the file.

![](/images/2021-11-28_1.png)

If everything is done correctly, the change should be applied immediately to the website.
To cancel the effect, one can simply remove the line `display: none;`.

Big thanks to KeeganT again for providing this awesome solution.
