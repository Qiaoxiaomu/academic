---
title: 'Probability Theory'
date: "2021-03-18"
type: book
weight: 1
math: true
---



# Sets and $\sigma$-algebras

## Sample Space $\Omega$

- $\Omega$ models all possible outcomes of an experiment
- elements of $\Omega$ are called **states** (of the world/nature) or points
- a state is denoted by $\omega$, $\omega \in \Omega$
- $A$ subset of $\Omega$ is a collection $A$ of stats taken from $\Omega$: $A \subset \Omega$

The **complement** of $A$: $A^{c}=\{\omega \in \Omega: \omega \notin A\}$

The **intersection** of $A$ and $B$: $A \cap B=\{\omega \in \Omega: \omega \in A \text { and } \omega \in B\} \subset \Omega$

The **union** of $A$ and $B$: $A \cup B=\{\omega \in \Omega: \omega \in A \text { or } \omega \in B\} \subset \Omega$

## Power Set $\mathscr{P}$

{{% callout note %}}
**Definition**: 
The colleciton of all subsets of $\Omega$ is called the **power set** of $\Omega$ and is denoted by $\mathscr{P}(\Omega)$
{{% /callout %}}

$\mathscr{P}(\Omega)$ is itself a set, but its elements are sets. In other words, 

$$A \in \mathscr{P}(\Omega) \Longleftrightarrow A \subset \Omega$$

## $\sigma$-algebra $\mathscr{F}$

{{% callout note %}}
**Definition**:
A collection $\mathscr{F}$ of subsets of $\Omega$ is called a $\sigma$-algebra on $\Omega$ if: 

- $\Omega \in \mathscr{F}$
- if $A \in \mathscr{F} \text{ then } A^c \in \mathscr{F}$
- if {$A_{n}, n=1,2, \ldots$} is a sequence of members of $\mathscr{F}$, then $\underset{1 \leq n<\infty}{\bigcup} A_{n} \in \mathscr{F}$
{{% /callout %}}

**Interpretation**

- $\mathscr{F}$ is the **information** available from the experiment described by $\Omega$, i.e., after the experiment, any sets in $\mathscr{F}$ will be **revealed to be true of false**.
- If $\mathscr{F}$ and $\mathscr{G}$ are $\sigma$-algebras on $\Omega$ such that $\mathscr{F} \cup \mathscr{G}$, we say that $\mathscr{F}$ is a sub $\sigma$-algebra of $\mathscr{G}$, i.e., $\mathscr{G}$ contains more information than $\mathscr{F}$

**Properties**

If $\mathscr{F}$ is a $\sigma$-algebra on $\Omega$, then,
- $\varnothing \in \mathscr{F}$
- if $A,B \in \mathscr{F}, \text{ then } A \cup B \in \mathscr{F}$
- if {$A_{n}, n=1,2, \ldots$} is a sequence of members of $\mathscr{F}$, then $\underset{1 \leq n<\infty}{\bigcap} A_{n} \in \mathscr{F}$
- $\mathscr{F}$ contains any set obtained from usual operations on its sets (complement, intersection, union).

**Remarks**

- The collection $\{\varnothing,\Omega \}$ is the smallest $\sigma$-algebra over $\Omega$
- The collection $\mathscr{P}$ is the largest $\sigma$-algebra over $\Omega$
- There are cases in between these two extremes: for any $\sigma$-algebra $\mathscr{F}$
  $$\{\Omega, \varnothing\} \subset \mathscr{F} \subset \mathscr{P}(\Omega)$$
- Intersections of $\sigma$-algebras are $\sigma$-algebras, i.e., information in common
- Unions of $\sigma$-algebras are not necessarily $\sigma$-algebras

## Borel $\sigma$-algebra

### Borel $\sigma$-algebra on $\mathbb{R}$

{{% callout note %}}
**Definition**: 
Let $\Omega=\mathbb{R}$ and $\mathscr{C}$ be as follows:

$$\mathscr{C}=\{(-\infty,a]:a \in \mathbb{R}\}$$

Then $\sigma(\mathscr{C})$ is called the Borel $\sigma$-algebra over $\mathbb{R}$, and is denoted by $\mathscr{B}(\mathbb{R})$
{{% /callout %}}

- $\mathscr{B}(\mathbb{R})$ contains most interesting sets of real numbers
- However, it can be shown that $\mathscr{B}(\mathbb{R}) \neq \mathscr{P}(\Omega)$
- If not mentioned otherwise, the $\sigma$-algebra considered on $\mathbb{R}$ is $\mathscr{B}(\mathbb{R})$

### Borel $\sigma$-algebra on $I$

{{% callout note %}}
**Definition**:
Let $I$ be any interval in $\mathbb{R}$, $\Omega=I$ and define $\mathscr{B}(I)$ by

$$\mathscr{B}(I)=\{I \cap B: B \in \mathscr{B}(\mathbb{R})\}$$

Then $\mathscr{B}(I)$ is a $\sigma$-algebra over $I$, and it is called the Borel $\sigma$-algebra over $I$.
{{% /callout %}}

**NOTE**: The sets in $\mathscr{B}(I)$ are just the intersection of $I$ and the sets in  $\mathscr{\mathbb{R}}$.

## Probability Measure and Space

{{% callout note %}}
**Definition**: 
A **measurable space** is a couple $(\Omega, \mathscr{F})$ where:
1. $\Omega$ is a sample space
2. $\mathscr{F}$ is a $\sigma$-algebra on $\Omega$
{{% /callout %}}

{{% callout note %}}
**Definition**: 
A **probability (measure)** on a measurable space $(\Omega,\mathscr{F})$ is a function $P:\mathscr{F} \rightarrow [0,1]$ such that:
1. $P(\Omega)=1$
2. $P$ is **countably additive**: if $\{A_n,n=1,2,...\}$ is a sequence of pairwise disjoint sets in $\mathscr{F}$, then

$$P\left(\bigcup_{n=1}^{+\infty} A_{n}\right)=\sum_{n=1}^{+\infty} P\left(A_{n}\right)$$
{{% /callout %}}

We call the triplet $(\Omega,\mathscr{F},P)$ a **probability space**.

{{% callout note %}}
**Definition**: 
Let $(\Omega,\mathscr{F},P)$ is a probability space and fix $A \in \mathscr{F}$.

If $P(A)=1$, we say that the event $A$ occurs **almost surly**, usually abbreviated as 'a.s.', or '$P$-a.s.'
{{% /callout %}}

# Measurablility and Random Variables

## Preimage

{{% callout note %}}
**Definition**: 
Let $f: \Omega \rightarrow \Omega'$ and $A' \subset \Omega'$. The **preimage** set of $A'$ under $f$ 

$$f^{-1}(A')=\\{\omega \in \Omega: f(\omega) \in A^{\prime}\\} \subset \Omega$$
{{% /callout %}}

Note: $f^{-1}(A')$ is a subset of $\Omega$, while $A'$ is a subset of $\Omega'$. 

For example, let $f(w)=w$'s surname first letter and $\Omega=\\{\text{ students in class 2 }\\}$, $\Omega'=\\{\text{ A,B,C,D,...,Z }\\}$, $A'=\\{\text{ A,K,L }\\}$.

Then $f^{-1}(A')$ means all of the students in class 2 whose surenames' first letter are A,K,L.

{{% callout note %}}
**Definition**: 
Let $(\Omega,\mathscr{F})$ and $(\Omega',\mathscr{F}')$ be two measurable spaces. A map $f: \Omega \rightarrow \Omega'$ is said to be $\mathscr{F}/\mathscr{F}'$**-measurable** (or simple, measurable) if 

$$f^{-1}\left(A^{\prime}\right) \in \mathscr{F} \text { for all } A^{\prime} \in \mathscr{F}^{\prime}$$
{{% /callout %}}

If $\mathscr{F}$ is the power set, then $f^{-1}(\mathscr{F})$ must be part of the power set, i.e. any map $f$ is measurable.

## Random Variables

{{% callout note %}}
**Definition**: 
A **random variable** on a measurable space $(\Omega,\mathscr{F})$ is a map $X: \Omega \rightarrow \mathbb{R}$ which is $\mathscr{F}/\mathscr{B}(\mathbb{R})$ measurable. That is,

$$X^{-1}(B)=\\{\omega \in \Omega: X(\omega) \in B\\} \in \mathscr{F} \text { for all } B \in \mathscr{B}(\mathbb{R})$$
{{% /callout %}}

The value taken by $X$ depends on the prevailing state of nature
$$\omega \in \Omega \rightarrow X(\omega) \in \mathbb{R}$$

- a random variable $X$ represents an unkonwn quantity
- information in $\mathscr{F}$ contains information on $X$
- we just write $\\{X \in B\\}$ for $X^{-1}(B)$

**Proposition** 

Let $f:\Omega \rightarrow \Omega'$. If $\mathscr{F}'$ is a $\sigma$-algebra on $\Omega'$ then

$$\sigma(f)=\\{f^{-1}(A'): A' \in \mathscr{F}'\\}$$

is a $\sigma$-algebra on $\Omega$ called $\sigma$-algebra generated by $f$.

- $\sigma(f)$ is the smalledst $\sigma$-algebra on $\Omega$ that makes $f$ measurable $\sigma(f)/\mathscr{F}'$
- $f$ is $\mathscr{F}/\mathscr{F}'$ measurable if and only if $\sigma(f) \subset \mathscr{F}$

**2-dice Example**

$$\Omega=\\{(1,1),...,(6,6)\\}, \Omega'=\mathbb{R}$$

$$\mathscr{F}=\mathscr{P}(\Omega), \mathscr{F}'=\mathscr{B}(\mathbb{R})$$

Define that $X_1$ and $X_2$ as the outcome from the first and the second dice, $Z$ as the sum of the 2 dice

$$X_1:\Omega \rightarrow \mathbb{R}, X_1((3,4))=3$$

$$X_2:\Omega \rightarrow \mathbb{R}, X_2((3,4))=4$$

$$Z:\Omega \rightarrow \mathbb{R},Z((3,4))=7$$

$B \in \mathscr{B}(\mathbb{R})$, $X^{-1}_1(B)=\\{X_1 \in B\\}=\\{\omega \in \Omega:X_1(\omega) \in B\\} \in \mathscr{F}=\mathscr{P}(\Omega)$

$\sigma(X_1)$ means what information I have if I can only observe the first dice. $\sigma(X_2)$ means what information I have if I can only observe the second dice. $\sigma(Z)$ means what information I have if I can only observe sum of the 2 dice. Here we have just partial information.

## Distribution and Density

{{% callout note %}}
**Definition**: 
Let $X$ be a random variable on a probability space $(\Omega, \mathscr{F}, P)$. The **distribution** or law of $X$ under $P$ is the probability $P_X$ on $(\mathbb{R}, \mathscr{B}(\mathbb{R}))$ defined by

$$P_X(B)=P(X^{-1}(B)), \text{ for } B \in \mathscr{B}(\mathbb{R})$$
{{% /callout %}}

Note that $X^{-1}(B)=\\{\omega \in \Omega: X(\omega) \in B\\} \in \mathscr{F} \text { for all } B \in \mathscr{B}(\mathbb{R})$

{{% callout note %}}
**Definition**: 
Let $X$ be a random variable on a probability space $((\Omega, \mathscr{F}, P)$. The **cumulative distribution function (cdf)** of $X$ is the function $F_X: \mathbb{R} \rightarrow [0,1]$ defined by

$$F_X(x)=P_X((-\infty,x])=P(X \leq x)$$
{{% /callout %}}

{{% callout note %}}
**Definition**: 
A random variable $X$ is continuous if its cdf $F_X$ is continuous, that is $P(X=x)=0$ for all $x \in \mathbb{R}$

A continuous random variable has a **density** $f_X: \mathbb{R} \rightarrow [0,+\infty)$ if 
$$F_X(x)=\int_{-\infty}^{x}{f_X(u)\mathrm{d}u}$$
{{% /callout %}}


## Independence

{{% callout note %}}
**Definition**: 
Consider a probability space $(\Omega,\mathscr{F},P)$
- The sub $\sigma$-algebras $\\{\mathscr{F}: t \in T\\}$ of $\mathscr{F}$ are independent if for all $t\_1,...,t\_n \in T$ and all $A\_1 \in \mathscr{F}\_{t_1},...,A_n \in \mathscr{F}\_{t_n}$ the following factorization property holds:
  $$P(A\_1 \cap ... \cap A\_n)=P(A\_1)·...·P(A\_n)$$
- Then random variables $\\{X\_t: t \in T\\}$ are independent if the generated $\sigma$-algebras $\\{\sigma(X_t): t \in T\\}$ are independent.
{{% /callout %}}

# Integration and Expectation

{{% callout note %}}
**Definition**: 
For an integrable random variable $X$ on $(\Omega,\mathscr{F},P)$ and a measurable set $A \in \mathscr{F}$, the integral of $X$ over $A$ is 

$$E[X;A]=\int_{A}{X}\mathrm{d}(P)=E[X\mathbb{I}_{A}]$$
{{% /callout %}}

$E[X;A]=E[X·\mathbb{I}_{A}]$. It's like considering $X$ only over the set $A$ and not over teh entire sample space. The effect of multiplying by the indicator is essentially killing the random variable $X$ outside $A$

**Properties**

$X,Y$ are integrable random variables on $(\Omega,\mathscr{F},P)$
- Linearity
- Monotonicity: if $X \leq Y$ a.s. then $E\[X\] \leq E[Y]$
- **Jensen Inequality**: if $I$ is an interval and 
  - $g: I \rightarrow \mathbb{R}$ is convex
  - $X \in I$ a.s.
  - $g(X)$ is integrable
  
  then $E[g(X)] \geq g(E[X])$. For example, $E[X^2] \geq E[X]^2, E[e^X] \geq e^{E[X]}$

# Conditional Expectation

## Kolmogorov Theorem

Let $X$ be an integrable random variable oin$(\Omega,\mathscr{F},P)$ and $\mathscr{G} \subset \mathscr{F}$ a sub $\sigma$-algebra of $\mathscr{F}$. Then, there exists a random variable $Z$ such that

1. $Z$ is $\mathscr{G}$-measurable: 
2. $Z$ is integrable
3. For all $A \in \mathscr{G}$, average of $Z$ over $A$ equals the average of $X$ over $A$, i.e.
   $$\int_{A}{Z \mathrm{d}(P)}=\int_{A}{X \mathrm{d}(P)}$$

Moreover, $Z$ is **unique**: if $\bar{Z}$ is any other random variable having the 3 properties above, then $Z=\bar{Z}, P-a.s.$

{{% callout note %}}
**Definition**: 
We call the random variable $Z$ in the previous Theorem the **conditional expectation** of $X$ with repect to $\mathscr{G}$, and we denote it by $E[X|\mathscr{G}]$ (which is a random variable!)
{{% /callout %}}

- $E[X|\mathscr{G}]$ means the best assessment you can make of $X$ given that you have the information contained in $\mathscr{G}$ which is a sub $\sigma$-algebra.
- The third property is called **partial averaging**
  $$E[Z;A]=E[E[X|\mathscr{G}];A]]=E[X;A] \text{ for all } A \in \mathscr{G}$$
- When $\mathscr{G}=\sigma(Y)$ (see [Random Variables](#random-variables)) we just write $E[X|Y]$ for $E[X|\sigma(Y)]$
- $E[X|\mathscr{G}]$ is the best forecast of $X$ given the information in $\mathscr{G}$, i.e., the distance of $X$ from a $\mathscr{G}$-measurable random variable $Z$ is minimal when $Z=E[X|\mathscr{G}]$

## Properties

$X$ and $Y$ are integrable random varables on $(\Omega,\mathscr{F},P)$ and $\mathscr{G}$ a sub-$\sigma$-algebra of $\mathscr{F}$
- Linearity
- Monotonicity
- Jensen Inequality
- "Expectation of conditional expectation is an expectation": 
  $$E[E\[X|\mathscr{G}]]=E\[X]$$
- "Tower property": if $\mathscr{H}$ is a sub-$\sigma$-algebra of $\mathscr{G}$ ($\mathscr{H} \in \mathscr{G}$), then
  $$E\[E\[X|\mathscr{G}]|\mathscr{H}]=E\[X|\mathscr{H}] \text{ a.s. }$$
- if $X$ is independent of $\mathscr{G}$, i.e., $\sigma(X)$ and $\mathscr{G}$ are independent, then
  $$E\[X|\mathscr{G}]=E\[X]$$
- "Pulling-out known factors": if $Y$ is a $\mathscr{G}$-measurable random variable ($Y$ is like a constant in this situation) such that $XY$ is integrable, then
  $$E\[XY|\mathscr{G}]=YE\[X|\mathscr{G}] \text{ a.s. }$$

## Conditional Variance

If $X$ is square integrable, define

$$\mathrm{VAR}[X|\mathscr{G}\]=E[(X-E[X|\mathscr{G}])^2|\mathscr{G}]=E[X^2|\mathscr{G}]-E[X|\mathscr{G}]^2$$