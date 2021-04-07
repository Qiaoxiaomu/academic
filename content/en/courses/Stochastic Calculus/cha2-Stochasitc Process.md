---
title: 'Stochastic Process'
date: "2021-04-05"
type: book
weight: 5
math: true
---

# Introduction

{{% callout note %}}
**Definition**: Let $(\Omega,\mathscr{F},P)$ be a probability space. A **stochastic process** is a collection
$$X_t;t \in T$$
of random variables, where $T$ is an arbitrary set.
{{% /callout %}}

- When $T=\{0,1,2,...\}$ we have a discrete-time stochastic process
- When $T=[0, +\infty)$ we have a continuous-time stochastic process; shorthand: $\{X_t\}$

{{% callout note %}}
**Definition**: For each $\omega \in \Omega$, a mapping (or function) from $[0,+\infty)$ to $\mathbb{R}$ defined by 

$$t \rightarrow X_t(\omega)$$

called the **sample path** or **trajectory** of the process at $\omega$
{{% /callout %}}

- If we fix a state $\omega \in \Omega$, $X(\omega)$ becomes a number.
- If we fix a state $\omega \in \Omega$ and observe the random values of $X_t(\omega)$ as time evolves, we are looking at a sample path 
  $$t \rightarrow X_t(\omega)$$
- If we fix another state $\tilde{\omega} \in \Omega$, we will in general observe a different sample path 
  $$t \rightarrow X_t(\tilde{\omega})$$

**Example**

Suppose $X$ is a random variable and define 
$$X_t=(t+1)X$$

Fix $\omega \in \Omega$, 
$$X_t(\omega)=(t+1) X (\omega)$$

Since $X(\omega) \in \mathbb{R}$, the trajection is just a function of $t$ and is a straight line indeed.