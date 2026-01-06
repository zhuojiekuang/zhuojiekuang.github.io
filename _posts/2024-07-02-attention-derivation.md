---
title: "Scaled dot-product attention: shapes and why the softmax shows up"
date: 2024-07-02
permalink: /posts/scaled-dot-product-attention
tags:
  - Machine Learning
  - Deep Learning
  - Transformers
---

Transformers are built on **attention**, and the core primitive is scaled dot-product attention:

$$\mathrm{Attn}(Q,K,V) = \mathrm{softmax}\!\left(\frac{QK^\top}{\sqrt{d_k}}\right)V.$$

This post unpacks what this means (shapes) and gives an intuitive derivation for why the softmax-weighted average is the natural form.

### Step 0: define the objects and shapes

Let:

- Sequence length \(n\)
- Key/query dimension \(d_k\)
- Value dimension \(d_v\)

Collect token-wise queries/keys/values into matrices:

$$Q \in \mathbb{R}^{n\times d_k},\quad K\in\mathbb{R}^{n\times d_k},\quad V\in\mathbb{R}^{n\times d_v}.$$

The similarity matrix is:

$$S := QK^\top \in \mathbb{R}^{n\times n},\quad S_{ij} = \langle q_i, k_j\rangle.$$

Row \(i\) contains how much query token \(i\) “matches” each key token \(j\).

### Step 1: attention as a content-based mixture over values

For a fixed query \(q_i\), we want an output vector \(o_i\in\mathbb{R}^{d_v}\) that is a weighted combination of the values:

$$o_i = \sum_{j=1}^n a_{ij} v_j.$$

If we stack all \(o_i\) into \(O\in\mathbb{R}^{n\times d_v}\) and all \(a_{ij}\) into \(A\in\mathbb{R}^{n\times n}\), this becomes:

$$O = AV.$$

So attention reduces to constructing a good row-stochastic matrix \(A\) (each row sums to 1).

### Step 2: why softmax is the natural normalization

We want weights \(a_{ij}\) that:

- are nonnegative
- sum to 1 for each query \(i\)
- increase as similarity \(S_{ij}\) increases

The simplest monotone way to map arbitrary real scores to a simplex is softmax:

$$a_{ij} = \frac{\exp(s_{ij})}{\sum_{\ell=1}^n \exp(s_{i\ell})}.$$

This ensures \(a_{ij}\ge 0\) and \(\sum_j a_{ij}=1\) automatically.

### Step 3: an energy-based / maximum entropy view

There’s also a principled derivation: choose weights \(a_i\) on the simplex that trade off “matching score” and entropy:

$$
\max_{a_i \in \Delta^{n-1}}\; \sum_{j=1}^n a_{ij} s_{ij} \;+\; \tau\,H(a_i),
$$

where \(H(a_i) = -\sum_j a_{ij}\log a_{ij}\) and \(\tau>0\) controls how peaky the distribution is.

Using a Lagrange multiplier \(\gamma\) for the constraint \(\sum_j a_{ij}=1\), set derivatives to zero:

$$
\frac{\partial}{\partial a_{ij}}
\left(\sum_j a_{ij} s_{ij} - \tau\sum_j a_{ij}\log a_{ij} + \gamma\left(\sum_j a_{ij}-1\right)\right)=0.
$$

This gives:

$$s_{ij} - \tau(1+\log a_{ij}) + \gamma = 0
\;\;\Rightarrow\;\;
a_{ij} \propto \exp\left(\frac{s_{ij}}{\tau}\right).
$$

Normalizing over \(j\) yields:

$$a_{ij} = \mathrm{softmax}\left(\frac{s_{ij}}{\tau}\right)_j.$$

So attention weights arise as a **maximum-entropy distribution biased toward high dot products**.

### Step 4: why the scaling by \(\sqrt{d_k}\)

If \(q_i\) and \(k_j\) have components with variance \(\approx 1\), then the dot product \(\langle q_i,k_j\rangle\) has variance that grows with \(d_k\). Large variance makes softmax saturate (very peaky), which can hurt gradients.

Scaling:

$$\tilde{S} = \frac{QK^\top}{\sqrt{d_k}}$$

keeps the magnitude of logits more stable as \(d_k\) changes, improving optimization.




