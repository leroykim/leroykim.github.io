---
layout: post
title: Probability Recap
categories: [Probability, Statistics]
tags: [Probability, Statistics]
author: Dae-young Kim
comment: true
---

#### Conditional Probability
$$P(A \mid B)=\frac{P(B \mid A)P(A)}{P(B)}$$

- $$P(A)$$: the prior
- $$P(B \mid A)$$: the likelihood
- $$P(A \mid B)$$: the posterior
- $$P(A \mid B) = P(A)$$: A and B are Independent.
- $$P(A \cap B \mid C)=P(A \mid C)P(B \mid C)$$: A and B are conditionally independent on the occurence of the event C.
- Often has `given that`

#### Law of Total Probability
Formally, if $$B_1, B_2, \ldots , B_n$$ form a partition of the sample space (i.e., they are mutually exclusive and exhaustive events), then for any event $$A$$:

$$P(A)=\sum_iP(A \mid B_i)P(B_i)$$

It provides a convenient way to think about partitioning events. Often comes with `tree of outcomes`

#### Combination
$$
\left( \begin{array}{c}
n \\ k
\end{array} \right) = \frac{n!}{k!(n-k)!}
$$

#### Permutation
$$\frac{n!}{(n-k)!}$$


#### Probability Mass Function (PMF)
$$\sum_{x \in X}f_{X}(x)=1$$

#### Probability Density Function (PDF)
$$\int_{-\infty}^{\infty}f_{x}(x)dx = 1$$

#### Cumulative Distribution Function (CDF)
$$F_{X}(x) = p(X \leq x)$$

![CDF Plot](/img/cdf_plot.svg)

- $$F_{X}(x)$$: representation of the CDF of the random variable `X`.
- $$P(X \leq x)$$: the probability that `X` is less than or equal to `x`.
- The `CDF` accumulates probabilities as `x` increases.
  
The CDF satisfies the following properties:
1. $$F_X(x)$$ is non-decreasing.
2. $$\lim\limits_{x \to -\infty} F_X(x) = 0$$.
3. $$\lim\limits_{x \to \infty} F_X(x) = 1$$.

Discrete variables' `CDF`: $$F_{X}(x)=\sum_{k \leq x}p(k)$$

Continuous variables' `CDF`: $$F_{X}(x)=\int_{-\infty}^{x}p(y)dy$$