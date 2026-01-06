---
title: "Flow matching: learning a continuous-time transport without likelihoods"
date: 2024-06-30
permalink: /posts/flow-matching
tags:
  - Machine Learning
  - Deep Learning
  - Generative Models
---

Flow matching is a way to train continuous-time generative models by learning a velocity field \(v_\theta(x,t)\) that transports noise to data, without explicitly computing likelihoods or solving adjoint sensitivities during training.

This post derives the core supervised objective:

$$\mathbb{E}_{t,x}\left[\left\|v_\theta(x,t) - v^\star(x,t)\right\|_2^2\right]$$

where \(v^\star\) is a “target” velocity induced by a chosen interpolation (bridge) between a base distribution and the data distribution.

### Setup: a deterministic flow (ODE) model

Consider an ODE:

$$\frac{d}{dt}x_t = v_\theta(x_t,t), \quad t\in[0,1].$$

If we initialize \(x_0\sim p_0\) (e.g. standard Gaussian), the ODE defines a transport map from \(p_0\) to some distribution \(p_1\) at \(t=1\). We want \(p_1\) to match the data distribution \(p_{\text{data}}\).

### A bridge distribution via interpolation

Pick a coupling between \(x_0\sim p_0\) and \(x_1\sim p_{\text{data}}\). The simplest conceptual coupling is to sample \(x_0\) and \(x_1\) independently; more advanced couplings reduce variance, but the math below doesn’t depend on the details.

Define an interpolation (bridge) \(x_t = \psi(x_0, x_1, t)\). A common choice is a linear bridge:

$$x_t = (1-t)\,x_0 + t\,x_1.$$

Then the time-derivative is:

$$\frac{d}{dt}x_t = x_1 - x_0.$$

However, \(x_0,x_1\) are random given \(x_t\), so the correct *conditional* target field is the conditional expectation:

$$v^\star(x,t) := \mathbb{E}\left[\frac{d}{dt}x_t \,\middle|\, x_t=x\right].$$

For the linear bridge, this means:

$$v^\star(x,t) = \mathbb{E}[x_1 - x_0 \mid x_t=x].$$

### Why matching \(v^\star\) is the right objective

The distribution \(p_t\) induced by the random variable \(x_t\) evolves according to the continuity equation:

$$\partial_t p_t(x) + \nabla\cdot\left(p_t(x)\,v^\star(x,t)\right)=0.$$

If we run our model ODE with velocity field \(v_\theta\), the induced distribution \(\tilde{p}_t\) evolves as:

$$\partial_t \tilde{p}_t(x) + \nabla\cdot\left(\tilde{p}_t(x)\,v_\theta(x,t)\right)=0.$$

So if \(v_\theta(x,t)=v^\star(x,t)\) for all \(x,t\) (in a suitable sense), then the model’s path distribution matches the bridge’s marginals, and in particular \(\tilde{p}_1 = p_1 = p_{\text{data}}\).

### From conditional expectation to a supervised regression target

We cannot compute \(v^\star(x,t)\) in closed form in general, but we can obtain unbiased samples of the “raw” velocity \(\dot{x}_t\) from the bridge.

For each training example:

1. Sample \(x_1 \sim p_{\text{data}}\)
2. Sample \(x_0 \sim p_0\)
3. Sample \(t \sim \mathrm{Unif}[0,1]\)
4. Form \(x_t = (1-t)x_0 + t x_1\)
5. Compute the bridge velocity sample \(\dot{x}_t = x_1 - x_0\)

Then train via least squares:

$$
\min_\theta \;
\mathbb{E}\left[\left\|v_\theta(x_t,t) - \dot{x}_t\right\|_2^2\right].
$$

This looks like ordinary regression, but it is doing something subtle: the minimizer satisfies

$$v_\theta(x,t) \approx \mathbb{E}[\dot{x}_t \mid x_t=x],$$

which is exactly the conditional velocity \(v^\star(x,t)\).

### Sampling after training

After training, generate by sampling \(x_0\sim p_0\) and integrating:

$$\frac{d}{dt}x_t = v_\theta(x_t,t),\quad t:0\to 1.$$

The endpoint \(x_1\) is a generated sample.




