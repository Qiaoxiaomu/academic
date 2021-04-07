---
title: '04 Tests on Mean Vectors'
date: "2021-03-18"
type: book
weight: 5
math: true
---
[Homework 2 Possible Solutions](https://1drv.ms/u/s!AhPTUXN0QjiSznyugvp6vWiHG_-W?e=okA0Ag)

# Drawbacks of Univariate Tests

- Inflate the Type I error rate.
  
  $$\alpha=P(\text{ reject } H\_0|H\_0 \text{ true })$$
  
  $$\begin{aligned}
  \alpha\_{F}&=P(\text{ at least reject one } H\_0|H\_0 \text{ true }) \\\\
  &=1-P(\text{ not reject any }|H\_0 \text{ true }) \\\\
  &=1-(1-\alpha)^{p} 
  \end{aligned}$$
  
  Even if $\alpha$ is small (say, 0.05), $\alpha\_F$ would be very large (10) if $p$ is large. 
  
- Completely ignore the correlations among the variables.
- Multivariate test is more powerful than separately univariate tests: Small individual effects may combine to significantly joint effect.

# One-sample Test of $\boldsymbol{\mu}$

## With $\mathbf{\Sigma}$ Known

- Assumption: The p-varaite sample {$\mathbf{y}\_1,...,\mathbf{y}\_n$} i.i.d. from $N\_p(\boldsymbol{\mu},\mathbf{\Sigma})$

- Hypothesis:Only focus on tow-sided test : $H\_0: \mathbf{\mu}=\mathbf{\mu}\_0$ vs $H\_1: \mathbf{\mu} \neq \mathbf{\mu}\_0$


- Test statistic: 
  
  $$Z^{2}=n\left(\overline{\mathbf{y}}-\boldsymbol{\mu}\_{0}\right)^{\prime} \mathbf{\Sigma}^{-1}\left(\overline{\mathbf{y}}-\boldsymbol{\mu}\_{0}\right) \sim \chi^{2}(p) \text { under } H\_{0}$$

- Rejection region: 
  Reject $H\_0$ if $Z^{2}>\chi\_{\alpha}^{2}(p)$ at significance level $\alpha$

The acception region of multivariate test is a ellipse, while rectangular of univariate test.
We should use multivariate test for it has a definite distribution to rely on.
The points inside the ellipse but outside the rectangle illustrate the inflation of Type I error of univariate tests.

<div align=center><a href="https://imgtu.com/i/6grCu9"><img src="https://s3.ax1x.com/2021/03/18/6grCu9.jpg" alt="6grCu9.jpg" width=50% border="0"/></a></div>

## With $\mathbf{\Sigma}$ Unknown (Hotelling's $T^2$)

Hotelling's $T^2$ test statistics:
$$T^{2}=n\left(\overline{\mathbf{y}}-\boldsymbol{\mu}\_{0}\right)^{\prime} \mathbf{S}^{-1}\left(\overline{\mathbf{y}}-\boldsymbol{\mu}\_{0}\right)$$

Under $H\_0: \mathbf{\mu}=\mathbf{\mu}\_0$, $T^2$ follow Hotelling's $T^2$ distribution with 2 parameters $p$ and $n-1$

Remarks:

- We must have $n > p$ for the Hotelling's $T^2$ test, otherwise $\mathbf{S}$ is not reversible. 
  i.e. $\operatorname{rank}(\mathbf{S}) \leq \min(n-1,p)$
- Hotelling $T^2$ can be converted to $F$ distribution by
  $$\frac{n-p}{p(n-1)} T^{2}(p, n-1)=F(p, n-p)$$
- A $n$ increases, Hotelling's $T^2$ approaches $\chi^2$ distribuiton: $T^{2}(p, \infty)=\chi^{2}(p)$.

# Comparing $\mathbf{\mu}\_1$ and $\mathbf{\mu}\_2$

## Review of Univariate

**Independent Samples**

- Assumptions:
  $y\_{11}, \ldots, y\_{1 n\_{1}} \text { i.i.d. } N\left(\mu\_{1}, \sigma^{2}\right); y\_{21}, \ldots, y\_{2 m\_{2}} \text { i.i.d. } N\left(\mu\_{2}, \sigma^{2}\right)$ with the common unknown variance $\sigma^2$. Furthermore, $y\_{1i}$ and $y\_{2j}$ are **independent**, $i=1,2,...,n\_1$, $j=1,2,...,n\_2$

- Distribution: 
  $$\frac{\left(\bar{y}\_{1}-\bar{y}\_{2}\right)-\left(\mu\_{1}-\mu\_{2}\right)}{\sqrt{s\_{p l}^{2}\left(1 / n\_{1}+1 / n\_{2}\right)}} \sim t\left(n\_{1}+n\_{2}-2\right)$$

  where $s^2\_{pl}$ is the pooled sample estimate of $\sigma^2$:
  $$s\_{p l}^{2}=\frac{\left(n\_{1}-1\right) s\_{1}^{2}+\left(n\_{2}-1\right) s\_{2}^{2}}{n\_{1}+n\_{2}-2}=\frac{\sum\_{i=1}^{2} \sum\_{j=1}^{n\_{i}}\left(y\_{i j}-\bar{y}\_{i}\right)^{2}}{n\_{1}+n\_{2}-2}$$
  
- Test statistic:
  $$T=\frac{\bar{y}\_{1}-\bar{y}\_{2}}{s\_{p l} \sqrt{\frac{1}{n\_{1}}+\frac{1}{n\_{2}}}} \sim t\left(n\_{1}+n\_{2}-2\right) \text { when } \mu\_{1}=\mu\_{2}\left(\text { under } H\_{0}\right)$$

**Paired Samples**

- Assumption:
  $y\_{11},...,y\_{1n}$ i.i.d. with mean $\mu\_1$ and $y\_{21},...,y\_{2n}$ i.i.d. with mean $\mu\_2$. 
  $y\_{1i}$ is **related to/paired with** $y\_{2i}$, $i=1,...n$. $y\_{1i}-y\_{2i} \text{ i.i.d. } N(\mu\_d, \sigma^2)$, where $\mu\_d=\mu\_1-\mu\_2$

- Statistics:
  Estimate of $\mu\_d$: $\bar{d}=\sum\_{i=1}^{n} d\_{i} / n, \text { where } d\_{i}=y\_{1 i}-y\_{2 i}$
  Estimate of $\sigma^2$: $s\_{d}^{2}=\sum\_{i=1}^{n}\left(d\_{i}-\bar{d}\right)^{2} /(n-1)$

- Distribution:
  $$\frac{\bar{d}-\mu\_{d}}{s\_{d} / \sqrt{n}} \sim t(n-1)$$

- Test statistics:
  $$T=\frac{\bar{d}}{s\_{d} / \sqrt{n}} \sim t(n-1) \text { when } \mu\_{d}=0\left(\text { under } H\_{0}\right)$$

## Multivariate Independent Samples
- Assumption:
  The p-variate samples $\mathbf{y}\_{11},...,\mathbf{y}\_{1n\_1} \text{ i.i.d. } N\_p(\boldsymbol{\mu}\_1,\mathbf{\Sigma})$ and $\mathbf{y}\_{21},...,\mathbf{y}\_{2n\_2} \text{ i.i.d. } N\_p(\boldsymbol{\mu}\_2,\mathbf{\Sigma})$, with the common unknown cov matrix $\mathbf{\Sigma}$. $\mathbf{y}\_{1i}$ and $\mathbf{y}\_{2j}$ are **independent** for all $i=1,...,n\_1$ and $j=1,...,n\_2$

- Test statistic:
  $$T^{2}=\frac{n\_{1} n\_{2}}{n\_{1}+n\_{2}}\left(\overline{\mathbf{y}}\_{1}-\overline{\mathbf{y}}\_{2}\right)^{\prime} \mathbf{S}\_{p l}^{-1}\left(\overline{\mathbf{y}}\_{1}-\overline{\mathbf{y}}\_{2}\right)$$

  where $\mathbf{S}\_{p l}=\frac{\left(n\_{1}-1\right) \mathbf{S}\_{1}+\left(n\_{2}-1\right) \mathbf{S}\_{2}}{n\_{1}+n\_{2}-2}$ is unbiased estimate of $\mathbf{\Sigma}$.

- Characteristic form of $T^2$:
  $$T^{2}=\left(\overline{\mathbf{y}}\_{1}-\overline{\mathbf{y}}\_{2}\right)^{\prime}\left[\left(\frac{1}{n\_{1}}+\frac{1}{n\_{2}}\right) \mathbf{S}\_{p l}\right]^{-1}\left(\overline{\mathbf{y}}\_{1}-\overline{\mathbf{y}}\_{2}\right)$$
  
  Note that $n\_1+n\_2-2>p$ for $\mathbf{S}\_{pl}$ to be nonsingular.

- Null distribution of $T^2$:
  $$T^{2} \sim T^{2}\left(p, n\_{1}+n\_{2}-2\right) \text { under } H\_{0}$$

## After the Rejction of $T^2$

Possible procedures that could be uesd to check each variable following the rejection of $H\_0: \boldsymbol{mu}\_1=\boldsymbol{\mu}\_2$:

1. Univariate t test, one for each variable:
   $$T\_{j}=\frac{\bar{y}\_{1 j}-\bar{y}\_{2 j}}{\sqrt{\left[\left(n\_{1}+n\_{2}\right) /\left(n\_{1} n\_{2}\right)\right] s\_{i j}}}$$
   
   where $s\_{jj}$ is the $j$th diagnal element of $\mathbf{S}\_{pl}$.
2. Bonferroni correction: Use $t\_{\alpha/(2p)}(n\_1+n\_2-2)$ instead of $t\_{\alpha/2}(n\_1+n\_2-2)$ as the critical value. (Conservative) 
   To overcomet the drawback of inflation of Type I error of univariate t test.
   
3. Use $T\_{\alpha}\left(p, n\_{1}+n\_{2}-2\right)=\sqrt{T\_{\alpha}^{2}\left(p, n\_{1}+n\_{2}-2\right)}$

## Multivariate Paired Samples

- Assumption:
  The p-variate samples $\mathbf{x}\_i$ and $\mathbf{y}\_i$ are paired, $i=1,...,n$. The differences $\mathbf{d}\_i=\mathbf{y}\_i-\mathbf{x}\_i$ i.i.d from $N\_p(\boldsymbol{\delta}, \mathbf{\Sigma}\_d)$ where $\boldsymbol{\delta}=\boldsymbol{\mu}\_y-\boldsymbol{\mu}\_x$.

- Hypothesis: 
  $H\_0: \boldsymbol{\delta}=0, H\_1 \neq 0$

- Statistics:
  Estimation of $\boldsymbol{\delta}: \overline{\mathbf{d}}=\sum\_{i=1}^{n} \mathbf{d}\_{i}$
  Estimation of $\mathbf{\Sigma}\_d: \mathbf{S}\_{d}=\sum\_{i=1}^{n}\left(\mathbf{d}\_{i}-\overline{\mathbf{d}}\right)\left(\mathbf{d}\_{i}-\overline{\mathbf{d}}\right)^{\prime} /(n-1)$

- Test Statistics:
  $$T^{2}=n \overline{\mathbf{d}}^{\prime} \mathbf{S}\_{d}^{-1} \overline{\mathbf{d}} \sim T^{2}(p, n-1) \text { under } H\_{0}$$

# Other Topics

## $T^2$ Statistics

- Partial $T^2$ test: determine whether some of the variables are **redundant** in the presence of other variables in terms of separating the groups - in the spirit of a full and reduced model (lack of fit) test.
- Profile Analysis: When the variables $Y\_1,...,Y\_p$ in $\mathbf{y}$ are commensurate, the pattern obtained by plotting $\mu\_1,...,\mu\_p$ against the variable index and connecting the points is called a profile. We may use $T^2$ statistics to analyse a profile (e.g. compare teh means $\mu\_1,...,\mu\_p$) or compare two or more profiles

## Tests on Cov Matrix

To conduct the two-sample $T^2$ tests, the cov matrix of the two population need to be assumed equal.
 






