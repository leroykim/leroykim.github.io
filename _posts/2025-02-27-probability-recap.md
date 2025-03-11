---
layout: post
title: Probability Recap
categories: [Probability, Statistics]
tags: [Probability, Statistics]
author: Dae-young Kim
comment: true
---

## Basics
### Conditional Probability

$$P(A \mid B)=\frac{P(B \mid A)P(A)}{P(B)}$$

- $$P(A)$$: the prior
- $$P(B \mid A)$$: the likelihood
- $$P(A \mid B)$$: the posterior
- $$P(A \mid B) = P(A)$$: A and B are Independent.
- $$P(A \cap B \mid C)=P(A \mid C)P(B \mid C)$$: A and B are conditionally independent on the occurence of the event C.
- Often has `given that`

### Law of Total Probability
Formally, if $$B_1, B_2, \ldots , B_n$$ form a partition of the sample space (i.e., they are mutually exclusive and exhaustive events), then for any event $$A$$:

$$P(A)=\sum_iP(A \mid B_i)P(B_i)$$

It provides a convenient way to think about partitioning events. Often comes with `tree of outcomes`

### Combination

$$
\left( \begin{array}{c}
n \\ k
\end{array} \right) = \frac{n!}{k!(n-k)!}
$$

### Permutation

$$\frac{n!}{(n-k)!}$$


<!-- ### Random Variables

###  -->
