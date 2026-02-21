---
title: Linear Algebra for Machine Learning: A Geometric Intuition Guide
date: 2026-02-21 15:00:00 +0530
categories: [ML, Math]
tags: [linear-algebra, intuition, Machine Learning, Geometry, Intuition]
---

# Linear Algebra for Machine Learning: A Geometric Intuition Guide

Most of us learnt linear algebra backwards. we started with symbols.

- Vectors are introduced as columns of numbers.
- Matrices are grids of numbers.
- Multiplication becomes a mechanical procedure.

And somewhere along the way, the meaning disappears.

Linear algebra was never meant to be about numbers on a page. It is about how space itself can be stretched, rotated, compressed, and reshaped. Every matrix is not just an arrangement of numbers - it is an action. It takes the space you live in and transforms it. Once you see that, the formulas stop being something to memorize. They become something you recognize.

And this is exactly why linear algebra sits at the heart of machine learning. Neural networks, embeddings, attention mechanisms - all of them are, at their core, sequences of geometric transformations applied to space.

This article is about Explaining myself - rebuilding linear algebra from that perspective. Not as arithmetic, but as geometry. 

Lets follow the below roadmap.

![Roadmap to understand Linear Algebra Geometrically](/assets/lib/img/Roadmap.png)

<h2>Vectors</h2>

A vector is a fundamental building block of Linear Algebra.

Vectors can be defined in more than one context:
In *Physics*, Its a entity with a magnitude and a direction
In *Computers*, its just a fancy word for ordered lists
In *Math*, it can be a representation of a point in space

Lets say a vector, $v = \begin{bmatrix}4 \\ 3\end{bmatrix}$ can be represnted geometrically on the number lines as

![](/assets/lib/img/LA_1.png)

We can understand it as a representation on how to reach to the end of the tip of the vector starting from the origin. So to reach to the tip of above vector, we need to move 4 units on x-axis and 3 units on the y-axis and we reach there.

Same logic applies in three dimensional space as well,

![](/assets/lib/img/LA_2.png)


