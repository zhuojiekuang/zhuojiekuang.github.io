---
title: "DDPM training objective is denoising score matching"
date: 2024-06-28
permalink: /posts/ddpm-denoising-score-matching
tags:
  - Machine Learning
  - Deep Learning
  - Diffusion
---

Diffusion models are often presented as a variational bound, but the training loss used in practice (predicting noise with an MSE) can be derived as a form of **denoising score matching**.

This post derives the key identities:

- The forward noising process yields a closed-form marginal $$q(x_t\mid x_0)$$.
- Predicting noise $$\epsilon$$ with MSE is equivalent (up to scaling) to matching the score $$\nabla_{x_t}\log q(x_t)$$.

### Forward process: a tractable noising Markov chain

Define a forward diffusion:

$$q(x_t\mid x_{t-1}) = \mathcal{N}\!\left(\sqrt{1-\beta_t}\,x_{t-1}, \beta_t I\right).$$

Let $$\alpha_t := 1-\beta_t$$ and $$\bar{\alpha}_t := \prod_{s=1}^t \alpha_s$$.

A standard result is that the marginal is Gaussian:

$$q(x_t\mid x_0) = \mathcal{N}\!\left(\sqrt{\bar{\alpha}_t}\,x_0,\; (1-\bar{\alpha}_t)I\right).$$

Equivalently, we can sample with a single noise draw:

$$x_t = \sqrt{\bar{\alpha}_t}\,x_0 + \sqrt{1-\bar{\alpha}_t}\,\epsilon,\quad \epsilon\sim\mathcal{N}(0,I).$$

### The score of the forward conditional

Because $$q(x_t\mid x_0)$$ is Gaussian with mean $$\mu_t(x_0)=\sqrt{\bar{\alpha}_t}x_0$$ and variance $$\sigma_t^2 I = (1-\bar{\alpha}_t)I$$, its score w.r.t. \(x_t\) is:

$$
\nabla_{x_t}\log q(x_t\mid x_0)
=
-\frac{1}{1-\bar{\alpha}_t}\left(x_t-\sqrt{\bar{\alpha}_t}\,x_0\right).
$$

Using the reparameterization identity \(x_t-\sqrt{\bar{\alpha}_t}x_0 = \sqrt{1-\bar{\alpha}_t}\,\epsilon\), this becomes:

$$
\nabla_{x_t}\log q(x_t\mid x_0)
=
-\frac{1}{\sqrt{1-\bar{\alpha}_t}}\;\epsilon.
$$

So: **knowing the noise \(\epsilon\)** is equivalent to knowing the score of \(q(x_t\mid x_0)\), up to a simple scaling.

### What the model learns in practice: predicting noise

In DDPMs, we train a neural net \(\epsilon_\theta(x_t,t)\) and minimize:

$$
\mathbb{E}_{t\sim\mathrm{Unif}(\{1,\dots,T\}),\,x_0\sim q(x_0),\,\epsilon\sim\mathcal{N}(0,I)}
\left[\left\|\epsilon - \epsilon_\theta(x_t,t)\right\|_2^2\right],
$$

where \(x_t = \sqrt{\bar{\alpha}_t}x_0 + \sqrt{1-\bar{\alpha}_t}\epsilon\).

### Noise prediction ↔ score matching

From the score identity above, we can map noise predictions to a score estimate:

$$
s_\theta(x_t,t)
:=
\nabla_{x_t}\log q(x_t)
\approx
-\frac{1}{\sqrt{1-\bar{\alpha}_t}}\;\epsilon_\theta(x_t,t).
$$

Similarly, the true conditional score is:

$$
\nabla_{x_t}\log q(x_t\mid x_0)
=
-\frac{1}{\sqrt{1-\bar{\alpha}_t}}\;\epsilon.
$$

Therefore:

$$
\left\|\epsilon - \epsilon_\theta(x_t,t)\right\|_2^2
=
(1-\bar{\alpha}_t)\left\|\nabla_{x_t}\log q(x_t\mid x_0) - s_\theta(x_t,t)\right\|_2^2.
$$

So the ubiquitous “predict \(\epsilon\) with MSE” loss is exactly a **denoising score matching** objective (up to a known time-dependent weighting).

### Why this matters

This derivation explains why diffusion training looks like simple regression: the network is learning a score field (or equivalently a denoising direction) parameterized by time.




