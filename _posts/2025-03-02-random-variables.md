---
layout: post
title: Random Variables
categories: [Probability, Statistics]
tags: [Probability, Statistics]
author: Dae-young Kim
comment: true
---
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
- Great for deriving properties of `random variables`.
  
The CDF satisfies the following properties:
1. $$F_X(x)$$ is non-decreasing.
2. $$\lim\limits_{x \to -\infty} F_X(x) = 0$$.
3. $$\lim\limits_{x \to \infty} F_X(x) = 1$$.

Discrete variables' `CDF`: $$F_{X}(x)=\sum_{k \leq x}p(k)$$

Continuous variables' `CDF`: $$F_{X}(x)=\int_{-\infty}^{x}p(y)dy$$

#### Joint Probability Distribution
A `joint probability distribution` describes the probability of two (or more) random variables occurring together.

##### Discrete Varibales
$$P(X=x, Y=y)$$

##### Continuous Varibales
$$f_{X,Y}(x,y) = \frac{\sigma^2}{\sigma x \sigma y}P(X \leq x, Y \leq y)$$

#### Marginal Probability Distribution
A `marginal probability distribution` gives the probability of one variable **regardless of the other**. This **marginalizes out** $$Y$$ by summing (discrete) or integrating (continuous) over all possible values of $$Y$$.

##### Discrete Varibales
$$P(X=x) =  \sum_{y}P(X=x, Y=y)$$

##### Continuous Varibales
$$f_{X}(x)=\int_{-\infty}^{\infty}f_{X,Y}(x,y)dy$$