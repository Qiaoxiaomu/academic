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

The colleciton of all subsets of $\Omega$ is called the **power set** of $\Omega$ and is denoted by $\mathscr{P}(\Omega)$

$\mathscr{P}(\Omega)$ is itself a set, but its elements are sets. In other words, 

$$A \in \mathscr{P}(\Omega) \Longleftrightarrow A \subset \Omega$$

## $\sigma$-algebra $\mathscr{F}$

**Definition**
A collection $\mathscr{F}$ of subsets of $\Omega$ is called a $\sigma$-algebra on $\Omega$ if: 

1. $\Omega \in \mathscr{F}$
2. if $A \in \mathscr{F} \text{ then } A^c \in \mathscr{F}$
3. if {$A_{n}, n=1,2, \ldots$} is a sequence of members of $\mathscr{F}$, then $\underset{1 \leq n<\infty}{\bigcup} A_{n} \in \mathscr{F}$

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
