---
title: "Softmax cross-entropy gradient: why it becomes (p - y)"
date: 2024-06-27
permalink: /posts/softmax-cross-entropy-gradient
tags:
  - Machine Learning
  - Deep Learning
  - Optimization
---

In classification, a very common loss is **softmax + cross-entropy**. A famous result is that the gradient w.r.t. the logits is simply:

$$\nabla_{z}\,\mathcal{L} = p - y$$

where $$z \in \mathbb{R}^K$$ are logits, $$p = \mathrm{softmax}(z)$$ is the predicted class distribution, and $$y$$ is the one-hot label vector.

This post derives that identity carefully.

### Definitions

Let:

$$p_k = \frac{e^{z_k}}{\sum_{j=1}^K e^{z_j}}.$$

For a one-hot label vector $$y$$ (so $$y_c=1$$ for the correct class $$c$$, and $$y_k=0$$ otherwise), cross-entropy loss is:

$$
\mathcal{L}(z, y)
=
-\sum_{k=1}^K y_k \log p_k
=
-\log p_c.
$$

### Step 1: write loss directly in terms of logits

Since:

$$p_c = \frac{e^{z_c}}{\sum_{j=1}^K e^{z_j}},$$

we have:

$$
\begin{align*}
\mathcal{L}(z,y)
&= -\log\left(\frac{e^{z_c}}{\sum_{j} e^{z_j}}\right) \\
&= -z_c + \log\left(\sum_{j=1}^K e^{z_j}\right).
\end{align*}
$$

### Step 2: take the derivative w.r.t. a logit \(z_k\)

Differentiate term-by-term.

First term:

$$\frac{\partial}{\partial z_k}(-z_c) = -\mathbf{1}[k=c].$$

Second term:

$$
\frac{\partial}{\partial z_k}\log\left(\sum_{j=1}^K e^{z_j}\right)
=
\frac{1}{\sum_{j} e^{z_j}}\cdot e^{z_k}
=
\frac{e^{z_k}}{\sum_{j} e^{z_j}}
=
p_k.
$$

Combine them:

$$
\frac{\partial \mathcal{L}}{\partial z_k}
=
p_k - \mathbf{1}[k=c].
$$

Since $$y_k = \mathbf{1}[k=c]$$ for one-hot labels, this is exactly:

$$\frac{\partial \mathcal{L}}{\partial z_k} = p_k - y_k.$$

Vectorizing across all classes:

$$\nabla_{z}\,\mathcal{L} = p - y.$$

### Why this is such a nice gradient

This shows that training pushes:

- **Up** the logit of the correct class (because if $$y_c=1$$, then gradient component is \(p_c-1 \le 0\)).
- **Down** logits of incorrect classes (gradient components \(p_k \ge 0\)).

It also explains why many implementations fuse “softmax + cross entropy” into a single numerically-stable op: the final gradient depends only on \(p\) and \(y\), not on explicit Jacobians of softmax.


