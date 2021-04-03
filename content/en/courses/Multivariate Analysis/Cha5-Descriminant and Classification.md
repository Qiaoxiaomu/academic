---
title: '05 Discriminant and Classification'
date: "2021-04-03"
type: book
weight: 6
math: true
---

# Introduction

Discriminant analysis refers to the description of group separation.

Classfication analysis more refers to the prediction or allocation of a new observation to groups.


# Fisher's LDA Analysis

## For Two Populations

### Basic Settings

- Assumption:
  The two populations to be separated have the same cov matrix $\mathbf{\Sigma}$ but distinct mean vectors $\boldsymbol{\mu}\_1$ and $\boldsymbol{\mu}\_2$.
- Samples and statistics:
  The p-variate sample $\mathbf{y}\_{11},...,\mathbf{y}\_{1n\_1}$ has mean vector $\overline{\mathbf{y}}\_1$
- Goal
  Find a **linear combination** of the p variables such that the **statistical distance** between the two transformed group is maximized.

### Objective Function

The linear combinations of $\mathbf{y}$'s can be realized by $Z=\mathbf{a}'\mathbf{y}$:

$$\begin{aligned}
z\_{1 i}=\mathbf{a}^{\prime} \mathbf{y}\_{1 i}=a\_{1} y\_{1 i 1}+a\_{2} y\_{1 i 2}+\cdots+a\_{p} y\_{1 i p}, & i=1,2, \ldots, n\_{1} \\\\
z\_{2 i}=\mathbf{a}^{\prime} \mathbf{y}\_{2 i}=a\_{1} y\_{2 i 1}+a\_{2} y\_{2 i 2}+\cdots+a\_{p} y\_{2 i p}, & i=1,2, \ldots, n\_{2}
\end{aligned}$$

The goal is to fina $\mathbf{a}$ to maximize the statistical distance:

$$\frac{\left(\bar{z}\_{1}-\bar{z}\_{2}\right)^{2}}{s\_{z}^{2}}=\frac{\left[\mathbf{a}^{\prime}\left(\overline{\mathbf{y}}\_{1}-\overline{\mathbf{y}}\_{2}\right)\right]^{2}}{\mathbf{a}^{\prime} \mathbf{S}\_{p /} \mathbf{a}}$$

Then solution to this optimization is:

$$\mathbf{a}=\mathbf{S}\_{pl}^{-1}(\overline{\mathbf{y}}\_1-\overline{\mathbf{y}}\_2) \text{ or its multiple }$$ 

### Optimization

{{% callout note %}}
**Cauchy-Schwarz Inequility**

For all vectors $\mathbf{a}$ and $\mathbf{b}$ of an inner product space it is true that

$$(\mathbf{a}' \mathbf{b})^2 \leq (\mathbf{a}' \mathbf{a})(\mathbf{b}' \mathbf{b})$$

Suppose $\mathbf{B}$ is a systemmetric matrix, then the inquility becomes

$$(\mathbf{a}' \mathbf{b})^2 \leq (\mathbf{a}' \mathbf{B} \mathbf{a})(\mathbf{b}' \mathbf{B}^{-1} \mathbf{b})$$

Equality holds when $B^{\frac{1}{2}} \mathbf{a}=B^{-\frac{1}{2}} \mathbf{b}$
{{% /callout %}}

Cauchy-Schwarz Inequility implies that the square of the inner product should be no larger than the product of the each length.

For the optimization problem below, $\mathbf{b}$ is just $(\overline{\mathbf{y}}\_1-\overline{\mathbf{y}}\_2)$ and $\mathbf{B}$ is just $\mathbf{S}\_{pl}$. If we move $(\mathbf{a}' \mathbf{B} \mathbf{a})$ to the left side, then we get

$$\frac{(\mathbf{a}' \mathbf{b})^2}{(\mathbf{a}' \mathbf{B} \mathbf{a})} \leq \mathbf{b}' \mathbf{B}^{-1}\mathbf{b}=\left(\overline{\mathbf{y}}\_{1}-\overline{\mathbf{y}}\_{2}\right)^{\prime} \mathbf{S}\_{p l}^{-1}\left(\overline{\mathbf{y}}\_{1}-\overline{\mathbf{y}}\_{2}\right)$$

Equality holds when $\mathbf{a}=\mathbf{S}\_{pl}^{-1}(\overline{\mathbf{y}}\_1-\overline{\mathbf{y}}\_2)$. $\mathbf{a}' \mathbf{y}$ is the discriminant function.

**Remarks**
- Note that our goal is not to find a classifier to separate the two groups but to find a projection direction to maximize the distance after projection. In other words, the discriminant function coefficient tells the direction onto which the original data should be projected in order to achieve the maximum distance, not the direction that separates the two groups.
- To interpret the discriminant function, we are more commonly interested in assessing the contribution of the variables.
- Standardize the uncommensurate variables before doing the discriminant analysis.

## For Several Populations

### Basic Settings

Suppose now $g$ groups are under consideration. For the $k$th group $G\_k,k=1,...,g$, the sample is denoted $\mathbf{y}\_{k1},...,\mathbf{y}\_{kn\_k}$, with sample size $n\_k$ and sample mean $\overline{\mathbf{y}}\_k$. The overall mean $\overline{\mathbf{y}}=\frac{1}{g} \sum\_{k=1}^{g} \overline{\mathbf{y}}\_k$



### Obective function

The ratio of the "between-group variation" (**the variation among different group means**) and the "within-group variation" (**the sum  different groups' variations**) now becomes

$$\frac{\mathbf{a}^{\prime} \mathbf{B} \mathbf{a}}{\mathbf{a}^{\prime} \mathbf{W a}}=\frac{\mathbf{a}^{\prime}\left[\sum\_{k=1}^{g}\left(\overline{\mathbf{y}}\_{k}-\overline{\mathbf{y}}\right)\left(\overline{\mathbf{y}}\_{k}-\overline{\mathbf{y}}\right)^{\prime}\right] \mathbf{a}}{\mathbf{a}^{\prime}\left[\sum\_{k=1}^{g} \sum\_{i=1}^{n\_{k}}\left(\mathbf{y}\_{k i}-\overline{\mathbf{y}}\_{k}\right)\left(\mathbf{y}\_{k i}-\overline{\mathbf{y}}\_{k}\right)^{\prime}\right] \mathbf{a}} \tag{1}$$

### Optimization

{{% callout note %}}
**Lemma (Maximizationg Quadratic Forms on Unit Sphere)**

For any positive semidefinite symmetric matrix $\mathbf{B}$ with eigen-pairs $(\lambda\_k,\mathbf{e}\_k),k=1,...,p, \lambda\_1 \geq ... \geq \lambda\_p \geq 0$, we have

$$\max \_{\mathbf{x} \neq 0} \frac{\mathbf{x}^{T} \mathbf{B} \mathbf{x}}{\mathbf{x}^{T} \mathbf{x}}=\lambda\_{1}, \text { attained when } \mathbf{x}=\mathbf{e}\_{1}$$

$$\max \_{\mathbf{x} \perp \mathbf{e}\_{1}, \cdots, \mathbf{e}\_{k}} \frac{\mathbf{x}^{T} \mathbf{B} \mathbf{x}}{\mathbf{x}^{T} \mathbf{x}}=\lambda\_{k+1}, \text { attained when } \mathbf{x}=\mathbf{e}\_{k+1}$$

$$\min \_{\mathbf{x} \neq 0} \frac{\mathbf{x}^{T} \mathbf{B} \mathbf{x}}{\mathbf{x}^{T} \mathbf{x}}=\lambda\_{p}, \text { attained when } \mathbf{x}=\mathbf{e}\_{p}$$
{{% /callout %}}

Let $\mathbf{b}=\mathbf{W}^{\frac{1}{2}} \mathbf{a}$, then the denominator becomes $\mathbf{b}^{T}\mathbf{b}$. Then the objective function

$$\frac{\mathbf{a}^{\prime} \mathbf{B} \mathbf{a}}{\mathbf{a}^{\prime} \mathbf{W a}}=\frac{\mathbf{b}^{T} \mathbf{W}^{-\frac{1}{2}}{ \mathbf{B}\mathbf{W}^{-\frac{1}{2}} \mathbf{b}}}{\mathbf{b}^{T} \mathbf{b}} \triangleq \frac{\mathbf{b}^{T} \mathbf{D} \mathbf{b}}{\mathbf{b}^{T} \mathbf{b}}$$

where $\mathbf{D}=\mathbf{W}^{-\frac{1}{2}} \mathbf{B} \mathbf{W}^{-\frac{1}{2}}$ which is symmetric.

Let $(\lambda\_k,\mathbf{f}\_k),k=1,...,p$ be the ordered eigen-pairs of $\mathbf{D}$, then by the Lemma, the objective function is maximized when $\mathbf{b}=\mathbf{f}\_1$, i.e. $\mathbf{a}=\mathbf{W}^{-\frac{1}{2}} \mathbf{f}\_1$ and the maximum is $\lambda\_1$. Notice that $\mathbf{D} \mathbf{f}\_k=\lambda\_k \mathbf{f}\_k$, i.e.

$$\mathbf{W}^{-\frac{1}{2}} \mathbf{B} \mathbf{W}^{-\frac{1}{2}} \mathbf{f}\_k=\lambda\_k \mathbf{f}\_k \tag{2}$$

Multiplying $\mathbf{W}^{-\frac{1}{2}}$ to both sides of $(2)$, we get $\mathbf{W}^{-1} \mathbf{B}\left(\mathbf{W}^{-1} \mathbf{f}\_{k}\right)=\lambda\_{k}\left(\mathbf{W}^{-\frac{1}{2}} \mathbf{f}\_{k}\right)$.

Let $\mathbf{e}\_k=\mathbf{W}^{-\frac{1}{2}} \mathbf{f}\_k$, then $(\lambda\_k,\mathbf{e}\_k),k=1,...,p$ are ordered eigen-pairs of $\mathbf{W}^{-1} \mathbf{B}$. Therefore, the above $\mathbf{a}$ is indeed $\mathbf{e}\_1$, i.e., $(1)$ is maximumed when $\mathbf{a}$ is taken as the first eigenvector of $\mathbf{W}^{-1} \mathbf{B}$, and the maximum is $\lambda\_1$

Furthermore, by the Lemma, 

$$\max \_{\mathbf{b} \perp \mathbf{f}\_{1}} \frac{\mathbf{b}^{T} \mathbf{D} \mathbf{b}}{\mathbf{b}^{T} \mathbf{b}}=\lambda\_{2}$$

attained at $\mathbf{b}=\mathbf{f}\_2$, converting to $\mathbf{a}=\mathbf{e}\_2$. And so forth.

## LDA Theorem

{{% callout note %}}
Let $\lambda\_1,...,\lambda\_s > 0$ denote the $s \leq \min(g-1,p)$ nonzero eigenvalues of $\mathbf{W}^{-1} \mathbf{B}$ and $\mathbf{e}\_1,...,\mathbf{e}\_s$ are the corresponding eigen vectors. Then the coefficient vector $\mathbf{a}$ that maximizes the ratio $(1)$ is given by $\mathbf{a}=\mathbf{e}\_1$, and the maximum is $\lambda\_1$. The linear combination $\mathbf{e}'\_1 \mathbf{y}$ is called the sample first discriminant, and the choice $\mathbf{e}'\_2$ is called the sample second discriminant and so forth.
{{% /callout %}}

No matter how many dimensions we have (say, $p$ dimensions), we only need $g-1$ directions to do discriminant. Finally, we reduce $p$ dimensions to $g$ dimensions.

**Remarks**

- For several-population case, the "within-group" variation $\mathbf{W}/(n\_1+...+n\_g-g)=\mathbf{S}\_{pl}$ is the estimate of $\mathbf{\Sigma}$
- In terms of graphical display, the Fisher's LDA for several groups could reduce the dimension from a very large number ($p$) of characteristics to a relatively few linear combinations ($s$). This helps display relationships and possible groupings of the population.
- The Fisher's LDA does not require normality, but it assumes equal cov matrix for all the populations.