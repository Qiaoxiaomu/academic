---
date: "2021-03-06"
title: Lec 2 Critical Point and Optimizer
type: book
weight: 2
math: true
---


# Critical Point

## Local Minima and Saddle Point

Optimization fails when critical point appears.
Critical point: gradient is close to zero, including **local minima** and **saddle point**. If it's local minima, no way to go; if saddle point, can escape.

## Distinguish such two cases?

By Taylor Series Expansion: 

$$
L(\boldsymbol{\theta}) \approx L\left(\boldsymbol{\theta}^{\prime}\right)+\left(\boldsymbol{\theta}-\boldsymbol{\theta}^{\prime}\right)^{T} \boldsymbol{g}+\frac{1}{2}\left(\boldsymbol{\theta}-\boldsymbol{\theta}^{\prime}\right)^{T} \mathbf{H}\left(\boldsymbol{\theta}-\boldsymbol{\theta}^{\prime}\right)
$$

where $\boldsymbol{g}$ is the gradient vector, $\mathbf{H}$ is the Hessian matrix.

At the critical point, gradient is zero, so:

$$
L(\boldsymbol{\theta}) \approx L\left(\boldsymbol{\theta}^{\prime}\right)+\frac{1}{2}\left(\boldsymbol{\theta}-\boldsymbol{\theta}^{\prime}\right)^{T} \mathbf{H}\left(\boldsymbol{\theta}-\boldsymbol{\theta}^{\prime}\right) = L(\boldsymbol{\theta}')+\boldsymbol{v}^{T} \mathbf{H} \boldsymbol{v}
$$

For all $\boldsymbol{v}$:

- $\mathbf{H}$ is positive definite $\Leftrightarrow$ $\boldsymbol{v}^{T} \mathbf{H} \boldsymbol{v}>0$ $\Rightarrow$  Around $\boldsymbol{\theta}: L(\boldsymbol{\theta})>L(\boldsymbol{\theta}')$  $\Rightarrow$  **Local minima**
- $\mathbf{H}$ is negative definite $\Leftrightarrow$ $\boldsymbol{v}^{T} \mathbf{H} \boldsymbol{v}<0$ $\Rightarrow$  Around $\boldsymbol{\theta}: L(\boldsymbol{\theta})>L(\boldsymbol{\theta}')$  $\Rightarrow$  **Local maxima**
- $\boldsymbol{v}^{T} \mathbf{H} \boldsymbol{v}>0$ or $\boldsymbol{v}^{T} \mathbf{H} \boldsymbol{v}<0$ $\Rightarrow$ **Saddle point**

## Deal with Saddle Point

If saddle point appears, $\mathbf{H}$ may tell the update direction. The process is：

1. Find the negative eigen value $\lambda < 0$ and its eigen vector $\boldsymbol{u}$ of $\mathbf{H}$ $\Rightarrow$
   $$\begin{array}{c}
    \boldsymbol{u}^{T} \mathbf{H} \boldsymbol{u}=\boldsymbol{u}^{T}(\lambda \boldsymbol{u})&=\lambda\|\boldsymbol{u}\|^{2} \\\\
    <0 & <0 \end{array}$$
2. Set $\boldsymbol{\theta}-\boldsymbol{\theta}^{\prime}=\boldsymbol{u} \Rightarrow \boldsymbol{\theta}=\boldsymbol{\theta}^{\prime}+\boldsymbol{u}$ 
3. $L(\boldsymbol{\theta}) \approx L\left(\boldsymbol{\theta}^{\prime}\right)+\frac{1}{2}\left(\boldsymbol{\theta}-\boldsymbol{\theta}^{\prime}\right)^{T} H\left(\boldsymbol{\theta}-\boldsymbol{\theta}^{\prime}\right) \Rightarrow L(\boldsymbol{\theta})<L\left(\boldsymbol{\theta}^{\prime}\right)$

# Batch

## Optimization with Batch

1. Divede the training data into $N$ batches, each batch includes $B$ samples.
2. Randome pick initail values $\boldsymbol{\theta}^{0}$ and do gradient descent for each batch
3. Computing all batches is called one **epoch**. 

## Small or Large?

- Smaller batch requires longer time for one epoch
- Smaller batch is noisy, larger batch is powerful. 
- "Noisy" update is better for training. 
  Usually smaller batch size has better performance.

# Momentumn

## Vanilla Gradient Descent

$$
\begin{aligned}
\mathbf{w^1}=\mathbf{w^0}&-\eta \frac{\partial \mathrm{L}(\mathbf{w})}{\partial{\mathbf{w}}}|\_{\mathbf{w}=\mathbf{w^0}} \\\\
\mathbf{w^2}=\mathbf{w^1}&-\eta \frac{\partial \mathrm{L}(\mathbf{w})}{\partial{\mathbf{w}}}|\_{\mathbf{w}=\mathbf{w^1}} \\\\
\mathbf{w^3}=\mathbf{w^2}&-\eta \frac{\partial \mathrm{L}(\mathbf{w})}{\partial{\mathbf{w}}}|\_{\mathbf{w}=\mathbf{w^2}} \\\\
&... \\\\
\mathbf{w^{i+1}}=\mathbf{w^i}&-\eta \frac{\partial \mathrm{L}(\mathbf{w})}{\partial{\mathbf{w}}}|\_{\mathbf{w}=\mathbf{w^i}} \\\\
\end{aligned}
$$

## Momentumn Gradient Descent

Movement: **movement of last step** minus **gradient** at present.

$$\mathbf{m^1}=\lambda \mathbf{m^0}-\eta \mathbf{g^0} $$

$$\boldsymbol{\theta^1}=\boldsymbol{\theta^0}+\mathbf{m^1}$$

$$\mathbf{m^2}=\lambda \mathbf{m^1}-\eta \mathbf{g^1}$$

$$\boldsymbol{\theta^2}=\boldsymbol{\theta^1}+\mathbf{m^2}$$

$$\dotsb$$

where $\mathbf{m}^{0}$ is the movment at time $0$ and $\mathbf{m}^{1}$ is the movement at time $1$.

# Classification

## One-hot Vector

For example, if there are 3 classes, then set the one-hot vector as

$$\widehat{\boldsymbol{y}}=\left[\begin{array}{l}
1 \\\\
0 \\\\
0
\end{array}\right] \text { or }\left[\begin{array}{l}
0 \\\\
1 \\\\
0
\end{array}\right] \text { or }\left[\begin{array}{l}
0 \\\\
0 \\\\
1
\end{array}\right]$$

The output of the network should also be a one-hot vector.

## Cross-entropy

We don't ues MSE to assess the performance but cross-entropy:

$$e=-\sum\_{i} \widehat{y}\_{i} \ln y\_{i}^{\prime}$$

where $y\_i$ is the output of the network, $y\_i'$ is the output of softmax funciton.

# Online Videos (from youtube)

## Critical Point

{{<youtube QW6uINn7uGk>}}

## Batch and Momentum

{{<youtube zzbr1h9sF54>}}

## Classification (short version)

{{<youtube O2VkP8dJ5FE>}}










