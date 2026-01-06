---
title: "KKT conditions: optimality for constrained optimization"
date: 2024-07-01
permalink: /posts/kkt-conditions
tags:
  - Optimization
  - Machine Learning
  - Math
---

Many optimization problems in ML are constrained (norm balls, simplex constraints, margin constraints, etc.). The Karush–Kuhn–Tucker (KKT) conditions give a set of equations/inequalities that characterize optimal solutions.

This post derives the KKT conditions from the Lagrangian and highlights the most important concept: **complementary slackness**.

### Problem statement

Consider the primal problem:

$$
\begin{aligned}
\min_x \quad & f(x) \\
\text{s.t.}\quad & g_i(x) \le 0,\quad i=1,\dots,m \\
& h_j(x) = 0,\quad j=1,\dots,p.
\end{aligned}
$$

Assume \(f,g_i,h_j\) are differentiable.

### The Lagrangian

Introduce Lagrange multipliers \(\lambda \in \mathbb{R}^m\) and \(\nu \in \mathbb{R}^p\). The Lagrangian is:

$$
\mathcal{L}(x,\lambda,\nu) = f(x) + \sum_{i=1}^m \lambda_i g_i(x) + \sum_{j=1}^p \nu_j h_j(x).
$$

For inequality constraints \(g_i(x)\le 0\), we require \(\lambda_i \ge 0\).

### The dual function and weak duality

Define the dual function:

$$q(\lambda,\nu) := \inf_x \mathcal{L}(x,\lambda,\nu).$$

For any \(\lambda \ge 0\) and any \(\nu\), \(q(\lambda,\nu)\) is a lower bound on the primal optimum \(p^\star\). This is weak duality:

$$q(\lambda,\nu) \le p^\star.$$

### KKT conditions (first-order optimality)

Under constraint qualifications (e.g. Slater’s condition for convex problems), strong duality holds and the primal/dual optima are achieved. Then there exist multipliers \((\lambda^\star,\nu^\star)\) such that \(x^\star\) is optimal iff the following hold:

#### 1) Primal feasibility

$$g_i(x^\star) \le 0,\quad h_j(x^\star)=0.$$

#### 2) Dual feasibility

$$\lambda_i^\star \ge 0 \quad \forall i.$$

#### 3) Stationarity

Gradient of the Lagrangian w.r.t. \(x\) vanishes:

$$
\nabla_x \mathcal{L}(x^\star,\lambda^\star,\nu^\star)
=
\nabla f(x^\star) + \sum_{i=1}^m \lambda_i^\star \nabla g_i(x^\star) + \sum_{j=1}^p \nu_j^\star \nabla h_j(x^\star)
= 0.
$$

#### 4) Complementary slackness

For each inequality constraint:

$$\lambda_i^\star\, g_i(x^\star) = 0 \quad \forall i.$$

This single equation encodes an “either-or” logic:

- If constraint \(i\) is **inactive** (\(g_i(x^\star) < 0\)), then \(\lambda_i^\star = 0\).
- If constraint \(i\) is **active** (\(g_i(x^\star) = 0\)), then \(\lambda_i^\star\) can be non-zero.

### A geometric interpretation

Stationarity says the negative gradient \(-\nabla f(x^\star)\) lies in the cone spanned by gradients of active inequality constraints plus the span of equality-constraint gradients:

$$
-\nabla f(x^\star)
\in
\mathrm{cone}\{\nabla g_i(x^\star): i\in \mathcal{A}\}
\;+\;
\mathrm{span}\{\nabla h_j(x^\star)\},
$$

where \(\mathcal{A}=\{i: g_i(x^\star)=0\}\) is the active set.

This is why KKT conditions feel like “balancing forces”: the objective gradient is canceled by constraint gradients.




