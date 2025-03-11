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

---

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

![Binomial Distribution For Different P Values (N=10)](/img/binomial_distribution.svg)

The binomial probability mass function (PMF):

$$P(X=k) = \left( \begin{array}{c}n \\ k \end{array}\right) p^k(1-p)^{n-k}$$

Where:
- $$k$$ = number of successes ($$0 \leq k \leq n $$)
- $$n$$ = total number of trials
- $$p$$ = probability of success per trial
- $$\left( \begin{array}{c}n \\ k \end{array}\right) = \frac{n!}{k!(n-k)!}$$ = binomial coefficient, which counts the number of ways to choose $$k$$ successes from $$n$$ trials

##### Mean
$$E[X] = np$$
##### Variance
$$Var(X) = np(1-p)$$
##### Standard Deviation
$$\sigma X = \sqrt{np(1-p)}$$
##### Skewness
$$\frac{1-2p}{\sqrt{np(1-p)}}$$
- If $$p=0.5$$, the distribution is symmetric. Otherwise, it is skewed.
- If $$p < 0.5$$, the distribution skews left.
- If $$p > 0.5$$, the distribution skews right. 
- The mean and variance determine the spread.

---

#### Poisson Distribution

The Poisson distribution models the number of events occurring in a fixed interval of time or space, assuming that:
- Events occur independently of each other.
- The average number of occurrences in a given interval is constant.

It is commonly used to model rare events such as:
- The number of earthquakes in a year.
- The number of customers arriving at a store per hour.
- The number of emails received per day.

![Poisson Distribution For Different Lambda Values](/img/poisson_distribution.svg)

If  $$X$$ follows a Poisson distribution with mean $$\lambda$$ (the expected number of occurrences in an interval), we write:

$$X \sim Poisson(\lambda)$$

The probability mass function (PMF) is:

$$P(X=k) = \frac{\lambda^k e^{-\lambda}}{k!}, \; k = 0,1,2, \ldots$$

Where:
- $$k$$ = number of occurrences
- $$\lambda$$ = expected number of occurrences in the interval
- $$e$$ = Euler's number ($$\sim 2.718$$)

The Poisson distribution is discrete, meaning $$k$$ can only take whole-number values.

##### Mean
$$E[X] = \lambda$$

##### Variance
$$Var(X) = \lambda$$

##### Standard Deviation
$$\sigma = \sqrt{\lambda}$$

##### Skewness
$$\frac{1}{\sqrt{\lambda}}$$

##### Insights
- The Poisson distribution models event occurrences in a fixed interval.
- The mean and variance are both equal to $$\lambda$$
- Smaller $$\lambda$$ values result in a distribution that is skewed right, while larger $$\lambda$$ values become more symmetric.
  
---

#### Uniform Distribution
The uniform distribution is a probability distribution where all outcomes are equally likely within a given range.

![Uniform Distribution For Different Intervals](/img/uniform_distribution.svg)