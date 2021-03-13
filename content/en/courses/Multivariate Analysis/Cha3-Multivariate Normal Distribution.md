---
date: "2021-03-11"
title: "03 Multivariate Normal Distribution"
type: book
weight: 4
math: true
---

# Introduction

## Multivariate Density Function

Remember that the output of a density function is a real number between $0-1$, i.e. $\mathbb{R}^{p} \stackrel{f}\longrightarrow \mathbb{R}$

If the p-variate random vector $\mathbf{y}=(Y\_1, ..., Y\_p)'$ follows the multivariate normal distribution with mean vector $\boldsymbol{\mu}$ and cov matrix $\mathbf{\Sigma}$, denoted as $\mathbf{y} \sim N\_p(\boldsymbol{\mu}, \mathbf{\Sigma})$, then the density function is

$$
f(\mathbf{y})=\frac{1}{(2 \pi)^{\frac{p}{2}}|\mathbf{\Sigma}|^{\frac{1}{2}}} e^{\frac{-(\mathbf{y}-\boldsymbol{\mu})^{\prime} \mathbf{\Sigma}^{-1}(\mathbf{y}-\boldsymbol{\mu})} {2}}
$$

## Bivariate Nomral Distribution

### Bivairate Density Function

$\boldsymbol{\mu}$ and $\mathbf{\Sigma}$ can be described as:

$$
\boldsymbol{\mu}=\left(\begin{array}{c}
\mu\_{1} \\\\
\mu\_{2}
\end{array}\right), \boldsymbol{\Sigma}=\left(\begin{array}{cc}
\sigma\_{1}^{2} & \rho\_{12} \sigma\_{1} \sigma\_{2} \\\\
\rho\_{12} \sigma\_{1} \sigma\_{2} & \sigma\_{2}^{2}
\end{array}\right)
$$
We say the random vector $\mathbf{y}=(Y\_1, Y\_2)'$ follows bivariate normal distribution, denoted as $\mathbf{y} \sim BN(\mu\_1,\mu\_2,\sigma\_1^2, \sigma\_2^2,\rho\_{12})$

### Contour Plot

Contour function describes the relationship between two variables assuming that the density holds constant. So in order to get contour function, we just need to set 

$$(\mathbf{y}-\boldsymbol{\mu})^{\prime} \mathbf{\Sigma}^{-1}(\mathbf{y}-\boldsymbol{\mu})=c^2$$

which could be simplified as 

$$
\left(\frac{y\_{1}-\mu\_{1}}{\sigma\_{1}}\right)^{2}+\left(\frac{y\_{2}-\mu\_{2}}{\sigma\_{2}}\right)^{2}-2 \rho\_{12}\left(\frac{y\_{1}-\mu\_{1}}{\sigma\_{1}}\right)\left(\frac{y\_{2}-\mu\_{2}}{\sigma\_{2}}\right)=c\_{1}^{2}
$$

Each of these ellipsoids is centered at $\boldsymbol{\mu}$ and has exes $\pm c\sqrt{\lambda\_j}e\_j$, where $(\lambda\_j,e\_j),j=1,2$ are eigenvalue and eigenvector pairs of $\mathbf{\Sigma}$

**One Possible Proof**:

By spectral decompostion, $\mathbf{\Sigma}=\sum{\lambda\_i \mathbf{e\_i} \mathbf{e\_i}'}$. 

Since the inverse matrix has the same eigenvector with inverse eighenvalue, thus $\mathbf{\Sigma}^{-1}=\sum{\frac{ \mathbf{e\_i}'}{\lambda\_i}}=\frac{ \mathbf{e\_1} \mathbf{e\_1}'}{\lambda\_1}+\frac{ \mathbf{e\_2} \mathbf{e\_2}'}{\lambda\_2}$

$$\begin{aligned}
c^2&=(\mathbf{y}-\boldsymbol{\mu})^{\prime} \mathbf{\Sigma}^{-1}(\mathbf{y}-\boldsymbol{\mu}) \\\\
&=(\mathbf{y}-\boldsymbol{\mu})^{\prime} (\frac{ \mathbf{e\_1} \mathbf{e\_1}'}{\lambda\_1}+\frac{ \mathbf{e\_2} \mathbf{e\_2}'}{\lambda\_2}) (\mathbf{y}-\boldsymbol{\mu}) \\\\
&=(\mathbf{y}-\boldsymbol{\mu})^{\prime} (\frac{ \mathbf{e\_1} \mathbf{e\_1}'}{\lambda\_1}) (\mathbf{y}-\boldsymbol{\mu})+(\mathbf{y}-\boldsymbol{\mu})^{\prime} (\frac{\mathbf{e\_2} \mathbf{e\_2}'}{\lambda\_2}) (\mathbf{y}-\boldsymbol{\mu})
\end{aligned}$$

Divide both sides of this equation by $c^2$, we can get:

$$(\mathbf{y}-\boldsymbol{\mu})^{\prime} (\frac{ \mathbf{e\_1} \mathbf{e\_1}'}{\lambda\_1 c^2}) (\mathbf{y}-\boldsymbol{\mu})+(\mathbf{y}-\boldsymbol{\mu})^{\prime} (\frac{ \mathbf{e\_2} \mathbf{e\_2}'}{\lambda\_2 c^2}) (\mathbf{y}-\boldsymbol{\mu})=1$$
By the definition of ellipse and ellipsoid, the axes should be $\pm (\frac{ \mathbf{e\_1} \mathbf{e\_1}'}{\lambda\_1 c^2})^{-\frac{1}{2}}=\pm c\sqrt{\lambda\_1} \mathbf{e\_1}$ and $\pm (\frac{ \mathbf{e\_2} \mathbf{e\_2}'}{\lambda\_2 c^2})^{-\frac{1}{2}}=\pm c\sqrt{\lambda\_2} \mathbf{e\_2}$

### Generalized Population Variance

$|\mathbf{\Sigma}|$ is called the generalized population variance. A small $|\mathbf{\Sigma}|$ indicates:

* then random vector $\mathbf{y}$ is concentrated close to $\boldsymbol{\mu}$ in p-space or

* there is multicollinearity amony the variables, i.e. the variables are highly intercorrelated.

# Properties of Random Vectors

- Linear Combination (omitted)
- Partitions (omitted)
- Independence of subvectors in $\mathbf{y}$ (omitted)
- Sum of 2 multivariate normal vectors (omitted)
- Conditional normality of subvectors in $\mathbf{y}$

  $$\mathbf{y}\_{1} \mid \mathbf{y}\_{2} \sim N\_{r}\left(\boldsymbol{\mu}\_{1}+\boldsymbol{\Sigma}\_{12} \boldsymbol{\Sigma}\_{22}^{-1}\left(\mathbf{y}\_{2}-\boldsymbol{\mu}\_{2}\right), \boldsymbol{\Sigma}\_{11}-\boldsymbol{\Sigma}\_{12} \boldsymbol{\Sigma}\_{22}^{-1} \boldsymbol{\Sigma}\_{21}\right)$$
  
  - $\mathbf{E}(\mathbf{y\_1}|\mathbf{y\_2})$ is a vector of linear functions of $\mathbf{y\_2}$, while $\mathbf{cov}(\mathbf{y\_1}|\mathbf{y\_2})$ doesn't depend on $\mathbf{y\_2}$
  - $\mathbf{\Sigma}\_{12} \mathbf{\Sigma}\_{22}^{-1}$ is called the matrix of regression coefficients when we regress $\mathbf{y\_1}$ on $\mathbf{y\_2}$
  

- Standardized vectors
  
  There are 2 ways to get the standardized vector $\mathbf{z}$:
  - $\mathbf{z}=\left(\mathbf{T}^{\prime}\right)^{-1}(\mathbf{y}-\boldsymbol{\mu})$, where $\mathbf{Y}$ is the nonsingular upeer trianular matrix from Cholesky decomposition of $\mathbf{\Sigma}$, s.t. $\mathbf{\Sigma}=\mathbf{T}' \mathbf{T}$
  - $\mathbf{z}=\left(\mathbf{\Sigma}^{1 / 2}\right)^{-1}(\mathbf{y}-\boldsymbol{\mu})$, where $\mathbf{\Sigma}=\mathbf{\Sigma}^{1/2} \mathbf{\Sigma}^{1/2}$
After standardization, $\mathbf{z}$ has mean $\mathbf{0}$ and cov matrix $\mathbf{I}$, i.e.
  
  $$\text { If } \mathbf{y} \sim N\_{p}(\boldsymbol{\mu}, \mathbf{\Sigma}), \text { then } \mathbf{z} \sim N\_{p}(\mathbf{0}, \mathbf{I})$$
  
- Quadratic form (Chi-square)

  According to the definition of Chi-square distribution, $\mathbf{z}^{\prime} \mathbf{z}=\sum\_{j=1}^{p} Z\_{j}^{2}$ forms a $\chi^2(p)$ random variable. Hence,
  
  $$\text { If } \mathbf{y} \sim N\_{p}(\mu, \mathbf{\Sigma}), \text { then }(\mathbf{y}-\boldsymbol{\mu})^{\prime} \mathbf{\Sigma}^{-1}(\mathbf{y}-\boldsymbol{\mu}) \sim \chi^{2}(p)$$
  
  Recall that the quadratic form is indeed the squared statistical/Mahalanbis distance
  
# Estimation in Multivariate Normal

## MLE of $\boldsymbol{\mu}$ & $\mathbf{\Sigma}$

The estimates of $\boldsymbol{\mu}$ & $\mathbf{\Sigma}$ can be found by maximizing the likelihood function based on the observation vectors $\mathbf{y}\_1,...,\mathbf{y}\_n$

$$\begin{aligned}
L\left(\mathbf{y}\_{1}, \mathbf{y}\_{2}, \ldots, \mathbf{y}\_{n}, \boldsymbol{\mu}, \mathbf{\Sigma}\right) &=\prod\_{i=1}^{n} f\left(\mathbf{y}\_{i}, \boldsymbol{\mu}, \mathbf{\Sigma}\right) \\\\
&=\prod\_{i=1}^{n} \frac{1}{(\sqrt{2 \pi})^{p}|\mathbf{\Sigma}|^{1 / 2}} e^{-\left(\mathbf{y}\_{i}-\boldsymbol{\mu}\right)^{\prime} \mathbf{\Sigma}^{-1}\left(\mathbf{y}\_{i}-\boldsymbol{\mu}\right) / 2} \\\\
&=\frac{1}{(\sqrt{2 \pi})^{n p}|\mathbf{\Sigma}|^{n / 2}} e^{-\sum\_{i=1}^{n}\left(\mathbf{y}\_{i}-\boldsymbol{\mu}\right)^{\prime} \mathbf{\Sigma}^{-1}\left(\mathbf{y}\_{i}-\boldsymbol{\mu}\right) / 2}
\end{aligned}$$

## Proof of MLE 

Take the logarithm of $L$

$$\ln{L}=-\frac{np}{2} \ln{2\pi}-\frac{n}{2}\ln{|\mathbf{\Sigma}|}-\frac{1}{2} \sum\_{i=1}^{n}{(\mathbf{y}\_i-\boldsymbol{\mu})'\mathbf{\Sigma}^{-1}(\mathbf{y}\_i-\boldsymbol{\mu})}$$
Then we can get the optimization problem

$$\max\_{\boldsymbol{\mu},\mathbf{\Sigma}} {\ln{L}}$$
The first order condition:

$$\begin{aligned}
\frac{\partial \ln L}{\partial \boldsymbol{\mu}}&=0 \\\\
\frac{\partial \ln L}{\partial \mathbf{\Sigma}}&=0 \\\\
\end{aligned}$$

For the estimation of $\boldsymbol{\mu}$,

$$\begin{aligned}
\frac{\partial \ln L}{\partial \boldsymbol{\mu}}&=-\frac{1}{2} \sum\_{i=1}^{n}{(\mathbf{y}\_i-\boldsymbol{\mu})\mathbf{\Sigma}^{-1}} \\\\
&=-\frac{1}{2}(\sum\_{i=1}^{n}{\mathbf{y}\_i}-\sum\_{i=1}^{n}{\boldsymbol{\mu}}) \mathbf{\Sigma}^{-1} \\\\
&=-\frac{1}{2}(\sum\_{i=1}^{n}{\mathbf{y}\_i}-n \boldsymbol{\mu}) \mathbf{\Sigma}^{-1} \\\\
&=0
\end{aligned}$$

Thus, $\sum\_{i=1}^{n}{\mathbf{y}\_i}-n \boldsymbol{\mu}=0$,

$$\boldsymbol{\mu}=\frac{1}{n}\sum\_{i=1}^{n}{\mathbf{y}\_i}=\overline{\mathbf{y}}$$

For the estimation of $\mathbf{\Sigma}$, situation becomes much more tedious and requires some complex matrix derivative technique. Detailed proof can be found [here](https://www.cnblogs.com/bigmonkey/p/11379144.html) (in Chinese). I'll make a simplified proof here.

$$\begin{aligned}
\frac{\partial \ln L}{\partial \mathbf{\Sigma}}&=-\frac{n}{2} \frac{\partial{\ln{|\mathbf{\Sigma}|}}}{\partial{\mathbf{\Sigma}}}-\frac{1}{2} \sum\_{i=1}^{n}{\frac{\partial{(\mathbf{y}\_i-\boldsymbol{\mu})'\mathbf{\Sigma}^{-1}(\mathbf{y}\_i-\boldsymbol{\mu})}}{\partial{\mathbf{\Sigma}}}} \\\\
&=-\frac{n}{2} \mathbf{\Sigma}^{-1}+\frac{1}{2} \sum\_{i=1}^{n}{{\mathbf{\Sigma}}^{-1} (\mathbf{y}\_i-\boldsymbol{\mu}) (\mathbf{y}\_i-\boldsymbol{\mu})' {\mathbf{\Sigma}}^{-1}} \\\\
&=0
\end{aligned}$$

Right Multiply both sides with $-\frac{1}{2} \mathbf{\Sigma}^{-1}$, we get

$$n \mathbf{I}=\sum\_{i=1}^{n}{{\mathbf{\Sigma}}^{-1} (\mathbf{y}\_i-\boldsymbol{\mu}) (\mathbf{y}\_i-\boldsymbol{\mu})'}$$

Left multiply both sides with $\mathbf{\Sigma}$, 

$$\mathbf{\Sigma}=\frac{1}{n} \sum\_{i=1}^{n}{(\mathbf{y}\_i-\boldsymbol{\mu}) (\mathbf{y}\_i-\boldsymbol{\mu})'}=\frac{n-1}{n} \mathbf{S}$$

## Sampling Distribution

The sample mean $\mathbf{y}=\sum\_{i=1}^{n}{\mathbf{y}\_i/n}$ follows:

$$\overline{\mathbf{y}} \sim N(\boldsymbol{\mu}, \frac{\mathbf{\Sigma}}{n})$$
The sample cov matrix, which is defined as $\mathbf{S}=\sum\_{i=1}^{n}\left(\mathbf{y}\_{i}-\overline{\mathbf{y}}\right)\left(\mathbf{y}\_{i}-\overline{\mathbf{y}}\right)^{\prime} /(n-1)$, follow

$$(n-1) \mathbf{S} \sim W\_{p}(n-1, \mathbf{\Sigma})$$
where $(n-1) \mathbf{S} \sim W\_{p}(n-1, \mathbf{\Sigma})$ denotes the Wishart distribution with n-1 degrees of freedom.

## Wishart Distribution

Suppose the p-variate vectors $\mathbf{z}\_i, i=1,...,q$ are i.i.d from $N\_p(\mathbf{0}, \mathbf{\Sigma})$, then $\sum\_{i=1}^{q}{\mathbf{z}\_i \mathbf{z}\_{i}'} \sim W\_p(q, \mathbf{\Sigma})$  

# Assessing Normality

## Univariate Nomrality

$H\_0$: The data are from normal
$H\_1$: The data are not from normal

### Shapiro-Wils Test

$$W=\frac{\left(\sum\_{i=1}^{n} a\_{(i)} y\_{(i)}\right)^{2}}{\sum\_{i=1}^{n}\left(y\_{i}-\bar{y}\right)^{2}}$$

- $\sqrt{W} \approx$ correlation between given data and normal scores.
- $\sqrt{W}=1$ when the data are perfectly normal
- $W$ significantly smaller than 1 indicates nonnormal

<!-- -->

``` r
set.seed(1230)
y1 <- rnorm(100);
y2 <- rexp(100, 2);
y3 <- rt(100, 1);
y4 <- -y2
shapiro.test(y1) # accept the null hypothesis
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  y1
    ## W = 0.98635, p-value = 0.3952
    
``` r
shapiro.test(y2) # reject the null hypothesis
```

    ## 
    ##  Shapiro-Wilk normality test
    ## 
    ## data:  y2
    ## W = 0.80837, p-value = 4.513e-10

### Kolmogorov-Smirnov (KS) Test

$$D=\sqrt{n} \sup \_{y}\left|F\_{n}(y)-F\_{0}(y)\right|$$

where $F\_{n}(y)$ is the empirical cdf from data, i.e. $F\_{n}(y)=\sum\_{i=1}^{n}I(X\_i \leq x)$, and $F\_{0}(y)$ is the cdf from the normal distribution with the same mean and var as the data.
Reject $H\_0$ for large $D$. $\sup$ means the largest number for all $y$.

``` r
ks.test(y1, "pnorm", mean(y1), sqrt(var(y1))) # accept H0
```

    ## 
    ##  One-sample Kolmogorov-Smirnov test
    ## 
    ## data:  y1
    ## D = 0.043044, p-value = 0.9925
    ## alternative hypothesis: two-sided

``` r
ks.test(y2, "pnorm", mean(y2), sqrt(var(y2))) # reject H0
```

    ## 
    ##  One-sample Kolmogorov-Smirnov test
    ## 
    ## data:  y2
    ## D = 0.1882, p-value = 0.001676
    ## alternative hypothesis: two-sided

### Cramer-von Mises (CVM) Test

KS test is not good if the data has extreme value.
  
$$C=\int\left[F\_{n}(y)-F\_{0}(y)\right]^{2} d F\_{0}(y)$$

```r
library(nortest)
cvm.test(y1) # accept H0
```

    ## 
    ##  Cramer-von Mises normality test
    ## 
    ## data:  y1
    ## W = 0.025708, p-value = 0.8987

```r
cvm.test(y2) # reject H0
```

    ## 
    ##  Cramer-von Mises normality test
    ## 
    ## data:  y2
    ## W = 1.1379, p-value = 7.37e-10

### Anderson-Darling Test

KS and CVM test can be affected by extreme value or tail value.

$$A=\int \frac{\left[F\_{n}(y)-F\_{0}(y)\right]^{2}}{F\_{0}(y)\left(1-F\_{0}(y)\right)} d F\_{0}(y)$$

```r
library(nortest)
ad.test(y1)
```

    ## 
    ##  Anderson-Darling normality test
    ## 
    ## data:  y1
    ## A = 0.24449, p-value = 0.7564

```r
ad.test(y2)
```

    ## 
    ##  Anderson-Darling normality test
    ## 
    ## data:  y2
    ## A = 6.5289, p-value = 3.969e-16

## Multivariate Normality

- Check whether each dimension of the vector is univariate normal
- Check whether any of the bivariate scatterplots violates the linearity
- Check the statistical distance {$d\_1,...d\_n$}, where

  $$d\_{i}=\left(\mathbf{y}\_{i}-\overline{\mathbf{y}}\right)^{\prime} \mathbf{S}^{-1}\left(\mathbf{y}\_{i}-\overline{\mathbf{y}}\right)$$
  
  to see if it is far from $\chi^{2}(p)$, via the Q-Q plot for $\chi^{2}(p)$. Applicable only for small p.