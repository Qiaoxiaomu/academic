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

$$\mathscr{C}=\{(-\inf,a]:a \in \mathbb{R}\}$$

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

# Probability Measure and Space

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
Let $(\Omega,\mathscr{F})$ and $\Omega',\mathscr{F}'$ be two measurable spaces. A map $f: \Omega \rightarrow \Omega'$ is said to be $\mathscr{F}/\mathscr{F}'$**-measurable** (or simple, measurable) if 

$$f^{-1}\left(A^{\prime}\right) \in \mathscr{F} \text { for all } A^{\prime} \in \mathscr{F}^{\prime}$$
{{% /callout %}}

If $\mathscr{F}$ is the power set, then $f^{-1}(\mathscr{F})$ must be part of the power set, i.e. any map $f$ is measurable.

## Random Variables

{{% callout note %}}
**Definition**: 
A **random variable** on a measurable space $(\Omega,\mathscr{F})$ is a map $X: \Omega \rightarrow \mathbb{R}$ which is $\mathscr{F}/\mathscr{B}(\mathbb{R})$ measurable. That is,

$$X^{-1}(B)=\{\omega \in \Omega: X(\omega) \in B\} \in \mathscr{F} \text { for all } B \in \mathscr{B}(\mathbb{R})$$
{{% /callout %}}

The value taken by $X$ depends on the prevailing state of nature
$$\omega \in \Omega \rightarrow X(\omega) \in \mathbb{R}$$

- a random variable $X$ represents an unkonwn quantity
- information in $\mathscr{F}$ contains information on $X$
- we just write {$X \in B$} for $X^{-1}(B)$

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