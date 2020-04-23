---
author: lydxlx
date: 2020-04-22
layout: post
title: "Equation of the circle passing through three points"
description: ""
mathjax: true
tipue_search_active: true
categories: math geometry
tags: computational-geometry circle template algorithm
---

* content
{:toc}

It is well known that any three non-collinear points (A, B, C) determine a unique circle passing through them. Mathematically, we can find the circle center by computing the intersection point of the perpendicular bisectors of segments AB and AC. (Pairs AB and BC or pairs AC and BC would also work.) In code implementation, however, this method can be error-prone and require extra handling when the segment slope is nearly vertical.

By searching the Internet carefully, I was finally able to find an algorithm that doesn’t deal with any slope computation, which is perfect for competitive programming. Please refer to [this link](http://www.ambrsoft.com/trigocalc/circle3d.htm) for the original post. In case the website goes down in the future, I cited its content in below. The copyright all belongs to ambrsoft.


---


The equation of an arbitrary circle can be described by the following equation:

$$
Ax^2 + Ay^2 + Bx + Cy + D = 0
$$

After substituting the three given points, $$(x_1, y_1), (x_2, y_2)$$ and $$(x_3, y_3)$$, which lie on the circle we get the set of equations that can be described by the determinant:

$$
\begin{vmatrix}
x^2 + y^2 & x & y & 1 \\
{x_1}^2 + {y_1}^2 & {x_1} & {y_1} & 1 \\
{x_2}^2 + {y_2}^2 & {x_2} & {y_2} & 1 \\
{x_3}^2 + {y_3}^2 & {x_3} & {y_3} & 1 \\
\end{vmatrix} = 0
$$


The coefficients $$A, B, C$$ and $$D$$ can be found by solving the following determinants:

$$
A = \begin{vmatrix}
{x_1} & {y_1} & 1\\
{x_2} & {y_2} & 1\\
{x_3} & {y_3} & 1\\
\end{vmatrix},
B = -\begin{vmatrix}
{x_1}^2+{y_1}^2 & {y_1} & 1\\
{x_2}^2+{y_2}^2 & {y_2} & 1\\
{x_3}^2+{y_3}^2 & {y_3} & 1\\
\end{vmatrix},
C = \begin{vmatrix}
{x_1}^2+{y_1}^2 & {x_1} & 1\\
{x_2}^2+{y_2}^2 & {x_2} & 1\\
{x_3}^2+{y_3}^2 & {x_3} & 1\\
\end{vmatrix},
D = -\begin{vmatrix}
{x_1}^2+{y_1}^2 & {x_1} & {y_1}\\
{x_2}^2+{y_2}^2 & {x_2} & {y_2}\\
{x_3}^2+{y_3}^2 & {x_3} & {y_3}\\
\end{vmatrix}
$$

The values of $$A, B, C$$ and $$D$$ will be after solving the determinants:
$$
A = {x_1}({y_2}-{y_3}) - {y_1}({x_2}-{x_3}) + {x_2}{y_3} - {x_3}{y_2}\\
B = ({x_1}^2+{y_1}^2)({y_3}-{y_2}) + ({x_2}^2+{y_2}^2)({y_1}-{y_3}) + ({x_3}^2+{y_3}^3)({y_2}-{y_1})\\
C = ({x_1}^2+{y_1}^2)({x_2}-{x_3}) + ({x_2}^2+{y_2}^2)({x_3}-{x_1}) + ({x_3}^2+{y_3}^2)({x_1}-{x_2})\\
D = ({x_1}^2+{y_1}^2)({x_3}{y_2}-{x_2}{y_3}) + ({x_2}^2+{y_2}^2)({x_1}{y_3}-{x_3}{y_1}) + ({x_3}^2+{y_3}^2)({x_2}{y_1} - {x_1}{y_2})
$$

---

Center point $$(x, y)$$ and the radius $$r$$ of the circle passing through $$({x_1}, {y_1}), ({x_2}, {y_2})$$ and $$({x_3}, {y_3})$$ are:

$$
x = -\frac{B}{2A} \\
y = -\frac{C}{2A}\\
r = \sqrt{\frac{B^2+C^2-4AD}{4A^2}}
$$


Here is the python code to find the circle center given three points (in format of pairs).
```python
    def center(A, B, C):
        (x1, y1), (x2, y2), (x3, y3) = A, B, C
        A = x1 * (y2 - y3) - y1 * (x2 - x3) + x2 * y3 - x3 * y2
        B = (x1 ** 2 + y1 ** 2) * (y3 - y2) + (x2 ** 2 + y2 ** 2) * (y1 - y3) + (x3 ** 2 + y3 ** 2) * (y2 - y1)
        C = (x1 ** 2 + y1 ** 2) * (x2 - x3) + (x2 ** 2 + y2 ** 2) * (x3 - x1) + (x3 ** 2 + y3 ** 2) * (x1 - x2)
        return (-B / A / 2, -C / A / 2)
```
