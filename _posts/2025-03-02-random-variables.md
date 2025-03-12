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

For a continuous random variable $$X$$ in the interval $$[a,b]$$, the probability density function (PDF) is:

$$f_{X}(x)=
    \begin{cases}
        \frac{1}{b-a}, & \text{if} \; a \leq x \leq b \\
        0, & \text{otherwise}
    \end{cases}$$

- $$a$$ and $$b$$ are the minimum and maximum values.
- The probability is uniformly spread across $$[a,b]$$.

The cumulative distribution function (CDF) is:

$$F_{X}(x)=
    \begin{cases}
        0, & x < a \\
        \frac{x-a}{b-a}, & \text{if} \; a \leq x \leq b \\
        1, & x > b
    \end{cases}$$

This shows the probability of $$X$$ being less than or equal to $$x$$.

##### Mean
$$E[X]=\frac{a+b}{2}$$

##### Variance
$$Var(X)=\frac{(b-a)^2}{12}$$

##### Standard Deviation
$$\sigma_{X}=\sqrt{\frac{(b-a)^2}{12}}$$

##### Entropy (Measure of Uncertainty)
$$H(X) = \ln(b-a)$$

##### Insights
- If $$X \sim U(a,b)$$, then any subinterval has an equal probability per unit length.
- Usages
  - Sampling (e.g., random number generation)
  - Hypothesis testing

---

#### Exponential Distribution

The exponential distribution models the time between independent events that happen at a constant rate.

![Exponential Distribution For Different Lambda Values](/img/exponential_distribution.svg)

A random variable $$X$$ follows an exponential distribution if the probability of waiting longer decreases exponentially as time passes:

$$X \sim \text{Exp}(\lambda)$$

Where:

- $$\lambda$$ = rate parameter, representing the average number of events per unit time.
- $$X$$ represents the time between events.

The probability density function (PDF) is:

$$f_X(x) =
\begin{cases}
\lambda e^{-\lambda x}, & x \geq 0 \\
0, & x < 0
\end{cases}$$

The cumulative distribution function (CDF) is:

$$F_X(x) =
\begin{cases}
1 - e^{-\lambda x}, & x \geq 0 \\
0, & x < 0
\end{cases}$$

This tells us that the probability of waiting at most $$x$$ time units is $$1-e^{-\lambda x}$$.

##### Mean
$$E[X] = \frac{1}{\lambda}$$

##### Variance
$$\text{Var}(X) = \frac{1}{\lambda^2}$$

##### Standard Deviation
$$\sigma_{X}=\frac{1}{\lambda^2}$$

##### Memorlyless Property
The probability of waiting for an additional time $$t$$, given that we have already waited $$s$$, is the same as starting fresh:

$$P(X>s+t \mid X>s) = P(X>t)$$

This makes the exponential distribution unique among continuous distributions.

##### Graph Explanation

- Yellow ($$\lambda = 0.5$$): Events occur less frequently, so longer times between events are more likely.
- Orange ($$\lambda=1$$): Moderate event frequency.
- Red ($$\lambda=2$$): Events occur more frequently, meaning shorter waiting times are more probable.

##### Insight
- As $$\lambda$$ increases, the probability of short waiting times increases.
- Usages: it is commonly used in waiting time problems,
  - Time between customer arrivals at a store.
  - Time until a machine breaks down.
  - Time between earthquakes.

#### Normal Distribution