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

---

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

##### Discrete variables'
$$F_{X}(x)=\sum_{k \leq x}p(k)$$

##### Continuous variables'
$$F_{X}(x)=\int_{-\infty}^{x}p(y)dy$$

---

#### Joint Probability Distribution
A `joint probability distribution` describes the probability of two (or more) random variables occurring together.

![Joint Probability Distribution Plot](/img/joint_pd_plot.svg)

##### Discrete Varibales
$$P(X=x, Y=y)$$

##### Continuous Varibales
$$f_{X,Y}(x,y) = \frac{\sigma^2}{\sigma x \sigma y}P(X \leq x, Y \leq y) = \int_{-\infty}^{\infty}\int_{-\infty}^{\infty}P(X \leq x, Y \leq y)dxdy$$

---

#### Marginal Probability Distribution
A `marginal probability distribution` gives the probability of one variable **regardless of the other**. This **marginalizes out** $$Y$$ by summing (discrete) or integrating (continuous) over all possible values of $$Y$$.

##### Discrete Varibales
$$P(X=x) =  \sum_{y}P(X=x, Y=y)$$

##### Continuous Varibales
$$f_{X}(x)=\int_{-\infty}^{\infty}f_{X,Y}(x,y)dy$$

---

#### Deriving a Marginal Probability Density Function (PDF) from a Joint PDF
The marginal probability density function is obtained by **integrating out** the unwanted variable from the joint probability density function.

The marginal PDF of $$X$$, which is $$F_{X}(x)$$, can be derived by intergrating out $$Y$$ from the joint PDF:

$$f_{X}(x)=\int_{-\infty}^{\infty}f_{X,Y}(x,y)dx$$

---

#### Conditioning PDFs on Other Variables
A **conditional PDF** describes the probability density of one variable **given that** another variable has a specific value.

For two continuous random variables $$X$$ and $$Y$$, the conditional probability density function (PDF) of $$X$$ given $$Y=y$$ is:

$$f_{X \mid Y}(x \mid y)=\frac{f_{X,Y}(x,y)}{f_{Y}(y)}$$

- The **conditional PDF** $$f_{X \mid Y}(x \mid y)$$ is computed by **dividing the joint PDF** $$f_{X,Y}(x,y)$$ **by the marginal PDF** $$f_{Y}(y)$$.
- It **rescales** the joint distribution to ensure the total probability for a given $$Y=y$$ sums to 1.

---

#### Binomial Distribution
The **binomial distribution** models the number of **successes** in a fixed number of independent **Bernoulli trials**, where each trial has **only two possible outcomes: success or failure**.

#### Uniform Distribution