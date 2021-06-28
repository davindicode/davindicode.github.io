---
layout: post
title: Bayesian Bessel
comments: true
thumbnail: bayes_bessel.jpg
categories: [Machine learning]
---

If you have ever gone through a basic statistics course or textbook, you are probably familiar with the concept of calculating the sample standard deviation in order to calculate the uncertainty in the sample mean. Whether you are crunching through balance sheets or reviewing freshly made measurements from the lab, this basic measure is used all over the place. There is however one peculiar aspect of the standard prescription: we need to divide by $N-1$ rather than $N$ as in the usual definition of variance, $N$ being the number of data points. This small and seemingly insignificant adjustment is known as *Bessel's correction*. Newcomers in statistics may be surprised to find out that this correction has a very simple mathematical derivation (at least I was). It is not just some empirical adjustment to account for the finite sample size, as often advertised. Even more, we can derive the same result from a Bayesian perspective using an approximation framework common in machine learning called *mean-field inference*.

## Data, statistics and estimators
Data is everywhere. We learn more about the world by observing this data, more precisely the processes that gave rise to the data seen. Whether you do not have complete knowledge about how the data is generated, or you believe nature is inherently stochastic (quantum mechanics anyone?), either way you end up with probability distributions. The field of statistics deals with inferring properties about a population given an observation of a subset of the population, called a sample. It uses the formal mathematical framework of probability theory to describe real world events.

An example that is used everywhere to explain these concepts is the task of estimating the mean height of people in a country: you will not be able to measure every single person, so an estimate has to be obtained from the measurements of a group of people.

Estimators are characterized mainly by three properties:
1. Consistency
2. Bias
3. Efficiency

A cool theorem called the Rao-Blackwell theorem 

## Bessel's correction

Now it turns out that we actually have a We also assume the data points drawn are statistically independent and identical, a common assumption denoted by i.i.d. (independent and identically distributed). 

$$
\begin{aligned}
\mathbb{E}[\hat{s}^2] &= \frac{1}{N} \mathbb{E}[\sum_i (x_i - \hat{\mu})^2] \\
&= \frac{1}{N} \mathbb{E}\left[\sum_i \left( (x_i - \mu) - \frac{1}{N}\sum_j (x_j - \mu) \right)^2 \right] \\
&= \frac{1}{N} \mathbb{E}\left[\sum_i (x_i - \mu)^2 - \frac{2}{N} \sum_j (x_j - \mu)^2 + \frac{1}{N^2} N\sum_j (x_j - \mu)^2 \right]\\
&= \frac{1}{N} \mathbb{E}\left[\left(1-\frac{1}{N} \right)\sum_i (x_i - \mu)^2 \right] = \frac{N-1}{N} \mathbb{E}[\hat{\sigma}^2]
\end{aligned}
$$

where we used $\mathbb{E}[\sum_{i \neq j} (x_i - \mu) (x_j - \mu) ]=0$ In fact, we made the independence assumption to get rid of the cross-terms.

$$
\begin{equation}\label{eq:bessel_corr}\tag{1}
\hat{\sigma}^2 = \frac{N}{N-1} \hat{s}^2 = \frac{1}{N-1}\sum_i (x_i - \hat{\mu})^2
\end{equation}
$$


## Bayesian perspective
As a Bayesian, our point of view onto this problem will be different. We considered the expectation of our estimators with respect to the distribution over all possible samples, i.e. repeating the same experiment an infinite number of times and taking the average like any good frequentist. Now how about not repeating the experiment so often? Let's take the observed sample as the truth given by the world, and explicitly state our modeling *assumptions* about how $x$ is generated.

As before, we describe the observations as drawing i.i.d. $x$ from a probability distribution $p(x)$. So far we have 

$$
\begin{equation}
p(\boldsymbol{x}) = \prod_i p(x_i)
\end{equation}
$$

Now we will introduce more specific structure to our model. Set a Gaussian $p(x \vert \mu,\sigma) = \mathcal{N}(\mu, \sigma^2)$, and note the conditioning onto the underlying distribution parameters which would be the population parameters for frequentists. Instead of attempting to find the true values of the parameters using specific functions of the data (our beloved estimators), we model the parameters as random variables drawn from a *prior* distribution. This distribution is chosen by us as part of the modeling assumptions and can be picked arbitrary. It reflects our prior knowledge (hence the name) about the model. The resulting distribution $p(x)$, where we do not observe the parameters, is obtained from marginalization 

$$
\begin{equation}
p(\boldsymbol{x}) = \int \prod_i p(x_i|\mu,\sigma^2) p(\mu,\sigma^2) \, \mathrm{d}\mu \, \mathrm{d}\sigma
\end{equation}
$$

which generally is intractable. Not only that, the result $p(x)$ depends significantly on the choice of our prior distribution.

How did the frequentists get away without any of this? Well actually, their situation is not that different. When frequentists test their models, under the name of hypothesis testing, the reference model introduces the modeling assumptions directly onto $p(x)$. Parameters are set to some values and this forms the null hypothesis. Under the null hypothesis, estimators have a *sampling* distribution (again, imagine repeating the experiment with $x$ drawn from the null hypothesis). This distribution is the equivalent of the prior used in the Bayesian framework, and indeed the null hypothesis is rejected if observations are very unlikely.


### Generalizations