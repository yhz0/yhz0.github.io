---
layout: post
date: 2022-02-11 19:55:27
title: "Ruszcynski Chapter 2 Exercises"
tags: ise630
katex: true
---

This is a written up solution for the exercises in Andrzej Ruszczynski's Nonlienar Optimization Exercise 2.15 - 2.20.

## 2.15

Define
$ f_j(x) = |y^j - \sum_{i=1}^n x_i u_i^j| $,
so $f(x) = \sum_{j=1}^N f_j(x)$.

Write $ f_j(x) = max\{y^j - \sum_{i=1}^n x_i u_i^j, \sum_{i=1}^n x_i u_i^j - y^j \} $
$$ \partial f_j(x) =
\begin{cases}
-u  & y^j - \sum_{i=1}^n x_i u_i^j > 0\\
\{\lambda u: \lambda \in [0, 1] \} & y^j - \sum_{i=1}^n x_i u_i^j = 0 \\
u & y^j - \sum_{i=1}^n x_i u_i^j < 0 \\
\end{cases}
$$

$$\partial f(x) = \sum_{j=1}^N \partial f_j(x)$$

Note, the sum is the Minkowski sum of $N$ sets.

## 2.16

Let $S = \{v \in [0, 1]^n: 1^\top v = k\} $; that is, an enumeration of zero-one vectors that has $k$ one component, and $n-k$ zero components.

$$f_k(x) = \max_{v\in \sigma} v^\top x$$

We see that $f_k$ is convex. Furthermore, $$\partial f_k(x) = conv \ \{v \in S: f_k(x) = v^\top x\} $$

## 2.17

Note for each $x$, $\lambda^\top Ax$ is linear in $\lambda$. Specifially, it is convex in $\lambda$, so taking pointwise-maximum results in convex function $F(\lambda)$.
$$\partial F(\lambda) = conv \ \bigcup_{x: F(\lambda) = \lambda^\top Ax} Ax$$

## 2.18

(I do not know how to solve this problem: from [Wikipedia](https://en.wikipedia.org/wiki/Convex_conjugate#Behavior_under_linear_transformations) it seems that $(fA)^{c}=A^{c} f^{c}$ holds, where $A^c = A^\top$ if $A$ is real matrix.)

$$
\begin{aligned}
g^*(y) &= \sup_x x^\top y - g(x) \\
&= \sup_x x^\top y - f(Ax) \\
\end{aligned}
$$

## 2.19

$$ f_*(y)=\sup_x x^\top y - \frac{1}{2} x^\top Ax = \frac{1}{2}y^\top A^{-1}y $$

$$B^{-1} - A^{-1} = A^{-1}(A-B)B^{-1} \succeq 0$$

## 2.20

$$
\begin{align*}
f(x) & = ||x||^2 - (\min_{z\in Z} ||x-z||)^2 \\
& = ||x||^2 - \min_{z\in Z} ||x-z||^2 \\
& = \max_{z \in Z} ||x||^2 - ||x-z||^2 \\
& = 2 \max_{z \in Z} x^\top z - \frac{1}{2} ||z||^2 \\
& = 2 g^*(x)
\end{align*}
$$

where
$$g(z) = \frac{1}{2} ||z||^2+I_Z(z)$$

$I_Z$ is the indicator function of set $Z$.

The second equation comes from the fact that $||x-z||$

and $||x-z||^2$

has the same minimizer $z$.
