---
layout: post
title: "Hello World"
date: 2018-10-26
categories: [Others]
tags: [Others]
---

<span style="color: gray;">Date: Oct 26, 2018</span>

This is the first post I created.

```c
#include <stdio.h>

int main() {
    printf("Hello, World!\n");
    return 0;
}
```

Notes from the original paper "RoFormer: Enhanced Transformer with Rotary Position Embedding" (Su et al., 2021) and its mathematical derivation.

> Rotary Position Embedding (RoPE) Mathematical Derivation begins with the basic rotary matrix definition. For a 2D rotation matrix:
>
> $$R_\theta = \begin{pmatrix} 
> \cos\theta & -\sin\theta \\
> \sin\theta & \cos\theta
> \end{pmatrix}$$
>
> For position m, frequency base $\theta$:
> $$\theta_m = m\theta$$
>
> Subsequently, in terms of complex number representation, RoPE can be expressed using complex numbers. For a complex number representation:
>
> $$q\cdot e^{im\theta} = (q_r + iq_i)(cos(m\theta) + i\sin(m\theta))$$
>
> This expands to:
> $$(q_r\cos(m\theta) - q_i\sin(m\theta)) + i(q_r\sin(m\theta) + q_i\cos(m\theta))$$
>
> Moving on to rotary embedding for query and key vectors, for a vector pair $(q, k)$ at position $m$:
>
> $$\Phi(q, m) = q \cdot e^{im\theta}$$
> $$\Phi(k, m) = k \cdot e^{im\theta}$$
>
> The dot product becomes:
> $$\Phi(q,m)^T\Phi(k,m) = (q \cdot e^{im\theta})^T(k \cdot e^{im\theta}) = q^Tk$$
>
> Furthermore, regarding frequency band definition, for dimension d and position m, the frequency band is:
>
> $$\theta_d = 10000^{-2d/D}$$
>
> where D is the total embedding dimension.
>
> The position-dependent frequency becomes:
> $$f_d(m) = m\theta_d = m \cdot 10000^{-2d/D}$$
>
> In the full rotary embedding implementation, for a vector $x$ of dimension $D$, RoPE pairs adjacent dimensions $(2d,2d+1)$:
>
> $$\begin{align*}
> y_{2d} &= x_{2d}\cos(m\theta_d) - x_{2d+1}\sin(m\theta_d) \\
> y_{2d+1} &= x_{2d}\sin(m\theta_d) + x_{2d+1}\cos(m\theta_d)
> \end{align*}$$
>
> As for the relative position property, for positions $m$ and $n$, the relative attention is preserved:
>
> $$\Phi(q,m)^T\Phi(k,n) = q^T\begin{pmatrix}
> \cos((m-n)\theta) & -\sin((m-n)\theta) \\
> \sin((m-n)\theta) & \cos((m-n)\theta)
> \end{pmatrix}k$$
>
> This shows that the attention score only depends on relative position $(m-n)$.
>
> Finally, considering key properties and advantages, the time complexity for sequence length $L$ and dimension $D$ is: $O(LD)$
>
> While the memory usage is independent of sequence length: $O(1)$
>
> This mathematical formulation shows that RoPE:
>
> - Encodes absolute positions
> - Naturally captures relative positions in attention computation
> - Has linear complexity
> - Requires no additional memory for position tables
> - Maintains rotational invariance in the embedding space
>
> The implementation combines rotary matrices with frequency-based position encoding, providing an efficient way to encode positional information in transformer architectures.

<figure style="margin: 0; padding: 0; text-align: center; margin-top: 21px; margin-bottom: 21px;">
  <img src="/assets/images/hello-world/shuncleopasfang.jpg" alt="shuncleopasfang" style="width: 20%;" />
  <figcaption style="margin-top: 0; color: gray; font-size: 0.9em; max-width: 64%; margin-left: auto; margin-right: auto; line-height: 1.2em;">shuncleopasfang</figcaption>
</figure>

<span style="color: gray;">Last updated: Sep 2023</span>