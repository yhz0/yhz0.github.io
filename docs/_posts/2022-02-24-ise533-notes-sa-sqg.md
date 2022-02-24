---
layout: post
date: 2022-02-24
title: "ISE 533 Notes 2020/02/24"
---

$$Min \ f(x): x\in X$$

where $x$ = decision (optimization) constrained = parameters of statistical models in ML

Unconstrained model: $X = R^n$.

## Constrained Problem

Let $\Pi_X(z)$ denote the projection of $z$ onto set $X$.

$$\Pi_X(z) := \argmin_{x\in X} ||x-z||^2 = \argmin_{x \in X} \sum_j (x_j - z_j)^2$$

$$
x^*(z) = \begin{cases}
z & z \in X \\
closest \ point \ in \ X & z \notin X
\end{cases}
$$

Projected Gradient Descent:
$$x^{k+1} = \Pi_X(x^k - \alpha_k \nabla f(x^k))$$

Example: $X =\{ x: L \leq x \leq U \}$

## SA and SQG

In Project 1, if the number of retailers is large, then you should use Stochastic Approximation.

- Stochastic Approximation (SA)
  - Differentiable
  - __Sub-differential__ exists (same as subgradient below)
- Stochastic Quasigradient (SQG)

In transshipment paper, the "gradients" are not quite gradients, but some pertubations, so it is SQG.

## Subgradients using Dual Multipliers

If $f$ is a convex function, then $v \in R^n$ is a __subgradient__ if $f(x)\geq f(\bar{x})+v(x-\bar{x})$.

$$
\begin{align*}
f(x, \omega) = & \min & g^\top &y \\
    &   s.t. & W &y = r(\omega) - T(\omega) x \\
    &     &  &   y \geq 0
\end{align*}
$$

$r(\omega) - T(\omega) x$ are random elements.

Dual form. $\pi$ is the dual multiplier.

$$
\begin{align*}
f(x, \omega) & = \max_\pi \{ (r(\omega) - T(\omega)x)^\top \pi :  W^\top \pi \leq g \} \\
& \geq \max_{\{\pi^1, \cdots, \pi^k\}} (r(\omega) - T(\omega)x)^\top \pi
\end{align*}
$$

If $\pi^1, \cdots, \pi^k$ satisfies $W^\top \pi^i \leq g$.

The last inequality is tight, if $\pi^1, \cdots, \pi^k$ are all extreme points of $W^\top\pi \leq g$,

If $f(\bar x, \omega) = (r(\omega) - T(\omega)x)^\top \bar\pi$, then $-\bar\pi^\top(T(\omega)\bar x)$ is a subgradient of $f(\bar x, \omega)$.
