---
date: "2021-01-01"
title: 01 Review of Algebra
type: book
weight: 2
math: true
---

# Basic Definitions and Operations

- matrix $\textbf{A}$, vector $\textbf{a}$, scalar $a$

- Special matrix: diagnal matrix diag($\textbf{A}$), identity matrix ($\textbf{I}$)

- Positive definite matrix: $\forall{\textbf{x}},\textbf{x}' \textbf{A} \textbf{x}>0$ 
  
  Positive semidefinite matrix: $\forall{\textbf{x}},\textbf{x}' \textbf{A} \textbf{x} \geq 0$

- **Length** of vector $\textbf{a}$: $L_{\textbf{a}}=\sqrt{\textbf{a}' \textbf{a}}=\sqrt{\sum_{i=1}^{n}{a_{i}^{2}}}$
  
  **Angle** between vectors $\textbf{a}$ and $\textbf{b}$: $\cos(\theta)=\frac{\textbf{a}'\textbf{b}}{L_{\textbf{a}} L_{\textbf{b}}}$
  
  **Projection** of vector $\textbf{a}$ onto $\textbf{b}$: $||\textbf{a}||\cos{\theta}·\frac{\textbf{b}}{||\textbf{b}||}=\frac{(\textbf{a}' \textbf{b})\textbf{b}}{\textbf{b}'\textbf{b}}$
  
# Characteristics of Matrices

## Rank and Inverse

- **Linear dependence** of vectors: $\textbf{a}\_1,..., \textbf{a}\_n$: if there exist constants $c_1,...,c_n$, not all zero, s.t. $\sum_{i=1}^{n}{c_i}\textbf{a}_{i}=0$.
  
- **Rank** of matrix $\textbf{A}$: number of linearly independent rows (or equivalently, columns) of $\textbf{A}$
  
- **Full rank**: if the rank of $\textbf{A}_{n×p}$ is the smaller of $n$ adn $p$.

- **Non-singular**: if $\textbf{A}$ is square and of full rank.

  **Singular**: if $\textbf{A}$ is square of less than full rank.

- **Inverse** of nonsingular square matrix $\textbf{A}$: a matrix $\textbf{A}^{-1}$ s.t. $\textbf{A}\textbf{A}^{-1}=\textbf{A}^{-1}\textbf{A}=\textbf{I}$
  
- **Orthogonal** matrix $\textbf{C}$: if $\textbf{C}' \textbf{C}=\textbf{C} \textbf{C}'=\textbf{I}$ or $\textbf{C}^{-1}=\textbf{C}'$

- **Trace** of n by n matrix $\textbf{A}=(a_{ij})_{n×n}$: $tr (\textbf{A})=\sum_{i=1}^{n}{a_{ii}}$:
  
  - $tr (\textbf{A} \pm \textbf{B})=tr(\textbf{A}) \pm tr(\textbf{B})$
  
  - $tr(c\textbf{A})=c·tr(\textbf{A})$
  
  - $tr(\textbf{A}\textbf{B})=tr(\textbf{B} \textbf{A})$
  
  - $tr(\textbf{A}'\textbf{A})=tr(\textbf{A}\textbf{A}')=\sum_{i=1}^{n}\sum_{j=1}^{p}{a_{ij}^2}$, where $\textbf{A}=(a_{ij})_{n×p}$

## Eigenvalue and Eigenvector

- **Eigenvalue** and **Eigenvector**: scalar $\lambda_{i}$ and nonzero vector $\textbf{x}_i$ s.t. $\textbf{A} \textbf{x}_i=\lambda_{i} \textbf{x}_{i}$, or $(\textbf{A}-\lambda_{i} \textbf{I})\textbf{x}_{i}=0, i=1,...,n$

  - $\textbf{A}=\sum_{i=1}^{n}{\lambda_{i}}, |\textbf{A}|=\prod_{i=1}^{n}{\lambda_{i}}$.
  
  - If $\textbf{A}>0$, then all $\lambda_i>0$.
  
  - If $\textbf{A} \geq 0$, then all $\lambda_i \geq 0$, and the number of positve $\lambda_i$ equal to the rank of $\textbf{A}$.
  
  - If $\textbf{A}$ i symmetric, then $x_i$'s are mutually orthogonal.

## Two Decomposition

-   **Spectral Decompostion**

    For a symmetric n by n matrix $\textbf{A}$ with the eigenvalue and
    normalized eigenvector pairs $(\lambda_i, \textbf{x}_{i}), i=1,...,n$, the spectral decomposition
    of A is:
    
    $$\mathbf{A}=\mathbf{C D C}^{\prime}=\sum_{i=1}^{n} \lambda_{i} \mathbf{x}_{i} \mathbf{x}_{i}^{\prime}$$

    where $\textbf{C}=(\textbf{x}_1,...,\textbf{x}_n)$ is orthogonal,
    and
    
    $$\mathbf{D}=\operatorname{diag}\left(\lambda_{1}, \ldots, \lambda_{n}\right)=\left(\begin{array}{cccc}
    \lambda_{1} & 0 & \cdots & 0 \\\\
    0 & \lambda_{2} & \cdots & 0 \\\\
    \vdots & \vdots & & \vdots \\\\
    0 & 0 & \cdots & \lambda_{n}
    \end{array}\right)$$

-   **Cholesky Decompostion**

    A *positive definite* matrix $\textbf{A}=(a_{ij})_{n×n}$ can be
    factored into $$\textbf{A}=\textbf{T}' \textbf{T}$$

    where $\textbf{T}$ is a *nonsingular upper triangular* matrix which
    can be got by `>chol(A)` in R

# R Impoementation

-   Addition and substraction:

``` r
A = matrix(1:12, nrow=4, ncol=3)
B = matrix(seq(3, 12, length=12), 4, 3)
A + B
```

    ##          [,1]     [,2]     [,3]
    ## [1,] 4.000000 11.27273 18.54545
    ## [2,] 5.818182 13.09091 20.36364
    ## [3,] 7.636364 14.90909 22.18182
    ## [4,] 9.454545 16.72727 24.00000

``` r
A - B
```

    ##           [,1]       [,2]       [,3]
    ## [1,] -2.000000 -1.2727273 -0.5454545
    ## [2,] -1.818182 -1.0909091 -0.3636364
    ## [3,] -1.636364 -0.9090909 -0.1818182
    ## [4,] -1.454545 -0.7272727  0.0000000

-   Transpose: Use the command `t()`, for example:

``` r
A = matrix(1:12, nrow=4, ncol=3)
t(A) # calculate the transpose of A
```

    ##      [,1] [,2] [,3] [,4]
    ## [1,]    1    2    3    4
    ## [2,]    5    6    7    8
    ## [3,]    9   10   11   12

-   Multiplication: Use the command `%*%`.
    
    A * B is not the usual matrix multiplication, it will multiply two matrices of the same shape element wisely.

``` r
A = matrix(1:12, nrow=4, ncol=3)
B = matrix(seq(3, 8, length=9), 3, 3)
A %*% B # matrix multiplication
```

    ##        [,1]  [,2]    [,3]
    ## [1,] 59.375  87.5 115.625
    ## [2,] 70.250 104.0 137.750
    ## [3,] 81.125 120.5 159.875
    ## [4,] 92.000 137.0 182.000

-   Inverse: Use the command `solve()`, for example:

``` r
A = matrix(rnorm(9), 3, 3) # create a 3*3 matrix whose entries are iid N(0, 1)
solve(A) # calculate the inverse of the matrix A
```

    ##            [,1]        [,2]         [,3]
    ## [1,] -0.2662734  0.71995765  0.007039622
    ## [2,]  1.0833418 -0.03265892 -0.033987117
    ## [3,] -0.5106006  0.12800571  0.444862362

-   Determinant: Use the command `det()` to calculate the determinante of a square matrix:

``` r
det(matrix(seq(1,3,length=9), 3, 3))
```

    ## [1] -1.665335e-16

-   Eigen-pairs and Spectral Decomposition:

``` r
A = matrix(rnorm(9), 3)
A = (A + t(A))/2 # to get a symmetric matrix
eigen(A) # do the decompositoin of A
```

    ## eigen() decomposition
    ## $values
    ## [1]  1.6040554  0.2125245 -3.7721759
    ## 
    ## $vectors
    ##            [,1]       [,2]       [,3]
    ## [1,] -0.3279015 0.86669085  0.3759356
    ## [2,]  0.4551679 0.49364058 -0.7410406
    ## [3,]  0.8278302 0.07187448  0.5563553
