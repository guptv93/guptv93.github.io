---
layout: default
title: Limit Theorems
slug: limit-theorems
item_num: 6
excerpt: Probability was introduced as the measure of likelihood of an event, but we've been picturing it as the frequency of occurrence of the event. Similarly, expected value was introduced as the weighted average of all possible values, but we've been thinking of it as the average value of a variable over multiple repetitions of the experiment. This note goes into why these are all valid assumptions.
---

$$
\newcommand{\expect}{\mathrm{E}}
\newcommand{\prob}{\mathrm{P}}
\newcommand{\v}{\mathrm{var}}
\newcommand{\Comb}[2]{ {}^{#1}C_{#2} }
$$

# Limit Theorems

#### Overview

When we introduced the topic of *Expected Value*, we introduced it as the average of all possible values that a random variable can take, weighted against the probability of each value. But we've been picturing Expected Value of a random variable as the average value of the random variable during multiple repetitions of the experiment. Similarly, probability was introduced as the measure of likelihood of an event (following the axioms of non-negativity, additivity and normalization) but we've been picturing it as the frequency of occurrence of the event. This short note goes into why these are valid assumptions. For a more detailed explanation, go through Chapter 5 of *Introduction to Probability.* 2nd ed. (Bertsekas, Dimitri, and John Tsitsiklis). 

#### The Weak Law of Large Numbers

The weak law of large numbers asserts that the sample mean of a large number of independent identically distributed random variables is very close to the actual mean of the distribution, with high probability.

We consider a sequence $X_1, X_2, \dots$ of independent identically distributed random variables with mean $\mu$ and variance $\sigma^2$, and define the sample mean by

$$
M_n = \frac{X_1 + \dots + X_n}{n}
$$

We have

$$
E[M_n] = \frac{E[X_1] + \dots + E[X_n]}{n} = \frac{n\mu}{n} = \mu
$$

and, using independence,

$$
\v(M_n) = \frac{\v(X_1 + \dots + X_n)}{n^2} = \frac{\v(X_1)+ \dots + \v(X_n)}{n^2} = \frac{n\sigma^2}{n^2} = \frac{\sigma^2}{n}
$$

We apply the Chebyshev inequality (proof in the textbook) and obtain:

$$
\begin{align}
\prob(|M_n - \mu| \geq \epsilon) &\leq \frac{\sigma^2}{n\epsilon^2}, & \textrm{for any } \epsilon > 0
\end{align}
$$

We observe that for any $\epsilon > 0$, the right-hand side of the above inequality goes to zero as $n$ increases. As a result we obtain the weak law of large numbers, that is stated below:

Let $X_1, X_2, \dots$ be independent identically distributed random variables with mean $\mu$. For every $\epsilon > 0$, we have  

$$
\begin{align}
\prob(|M_n - \mu| \geq \epsilon) &= \prob\bigg(\bigg|\frac{X_1 + \dots X_n}{n} - \mu\bigg| \geq \epsilon\bigg) \to 0, & \textrm{as } n \to \infty
\end{align}
$$

The weak law of large numbers states that for large $n$, the bulk of the distribution of $M_n$ is concentrated near $\mu$. In other words, the average value of the random variable (over multiple repetitions) converges to the expected value of the random variable in probability (as the number of repetitions goes to $\infty$).

#### Probabilities as Frequencies

Consider an event $A$ defined in the context of some probabilistic experiment. Let $p = \prob(A)$ be the probability (likelihood) of this event. We consider $n$ independent repetitions of the experiment, and let $M_n$ be the fraction of time that event $A$ occurs; in this context, $M_n$ is often called the **emperical frequency** of $A$. Note that

$$
M_n = \frac{X_1 + \dots + X_n}{n}
$$

where $X_i$ is $1$ whenever $A$ occurs, and $0$ otherwise; and $\expect[X_i] = p$. The weak law applies and shows that when $n$ is large, the empirical frequency is close to $p$ (in probability). Loosely speaking, this allows us to conclude that empirical frequencies are faithful estimates of $p$. Alternatively, we can interpret the probability $p$ of an event as its frequency of occurence.

#### Further Steps

*The Strong Law of Large Numbers* is very similar to *The Weak Law of Large Numbers*. The only difference is that the strong law tells us that the sample mean sequence deterministically converges to the expected value (instead of converging in probability), as the number of repetitions increases.

Go through *The Central Limit Theorem* as it has great importance in Classical Statistics. 