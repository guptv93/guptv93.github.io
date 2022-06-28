---
layout: default
title: Statistical Inference
slug: inference
item_num: 3
excerpt: We explore what "Statistical Inference" actually means. We formally define "Statistical Models", "Regression Functions", etc. and finally go over the difference between Classical Inference and Bayesian Inference.
---

$$
\newcommand{\expect}{\mathrm{E}}
\newcommand{\prob}{\mathrm{P}}
\newcommand{\v}{\mathrm{var}}
\newcommand{\Comb}[2]{ {}^{#1}C_{#2} }
\newcommand{\mff}{\mathfrak{F}}
$$

# Statistical Inference

Statistical Inference, or "learning" as it is called in computer science, is the process of using data to infer the distribution that generated the data. In some cases, we may want to infer only some feature/property of  the generating distribution.



## Statistical Models

A **statistical model** $\mff$ is a set of distributions (or densities or regression functions). A **parametric model** is a model that can be parameterized by a finite number of parameters. For example, if we assume that the data comes from a Normal distribution, then the model is 

$$
\mff = \bigg\{ f(x;\mu, \sigma) = \frac{1}{\sigma\sqrt{2\pi}}\mathrm{exp}\bigg[\frac{-(x-\mu)^2}{2\sigma^2}\bigg] : \mu \in \mathbb{R}, \sigma > 0\bigg\}
$$

This is a two-parameter model. In general, a parametric model takes the form

$$
\mff = \bigg\{f(x; \theta): \theta \in \Theta\bigg\}
$$

where $\theta$ is an unknown parameter (or vector of parameters) that can take values in the parameter space $\Theta$. A **nonparametric model** is a set $\mff$ that cannot be parameterized by a finite number of parameters. Given some data and some fixed model, the task of **statistical inference** is to find the distribution (or regression function) that best explains the data.



#### What is a Regression Function?

Suppose we observe pairs of data $(X_1, Y_1), \dots, (X_n, Y_n)$. Perhaps $X_i$ is the blood pressure of subject $i$ and $Y_i$ is how long they live. $X$  is called a **predictor** or **feature** or **independent variable**. $Y$ is called the **outcome** or the **response variable** or the **dependent variable**. We assume that there is some relationship between $Y$ and $X$ of the very general form $r(x) = \expect(Y \vert X = x)$. The function $r$ that connects the input variable to the output variable is in general unknown. The process of estimating $r$ (finding the best fit $f \in \mff$ for $r$) based on the available data is called **regression** or **curve estimation**. If we restrict the set $\mff$ so that it only contains the functions that can be completely described by a fixed set of parameters, then we have a **parametric regression model**. Every $f$ belonging to $\mff$ is called a **regression function**. 

Note that if $r(X) = \expect(Y \vert X)$, then

$$
Y = r(X) + \epsilon
$$

where $\expect(\epsilon \vert X) = 0$. To see this, define $\epsilon = Y - r(X)$. Then, taking conditional expectation on both sides:

$$
\begin{align}
\expect(\epsilon \vert X) &= \expect(Y \vert X) - \expect\big(r(X) \vert X\big) \\
&= \expect(Y \vert X) - r(X) \\
&= 0
\end{align}
$$

Also $\expect(\epsilon) = \expect\bigg(\expect(\epsilon \vert X)\bigg) = \expect(0) = 0$.



## Bayesian vs Classical Inference

Within the field of statistics there are two prominent schools of thought, with opposing views: the Bayesian and the Classical (also called Frequentist). We learnt that in parametric statistical inference, a model is fully specified, except for an unknown, possibly multidimensional, parameter $\theta$, which we wish to estimate. This parameter can be viewed as either a random variable (Bayesian approach) or as an unknown constant (Classical approach). The usual objective is to arrive at an estimate of $\theta$ that is close to the true value in some sense. 

The Bayesian approach views the distribution (or regression function) as chosen randomly from a given statistical model. The unknown parameters are treated as random variables with known prior distrubtions. We conduct an experiment, make some observation ($X$) and then try to infer the value of the random variable ($\Theta$) during the conducted experiment. We derive a posterior distribution $\prob(\Theta \vert X)$ which tells us how likely it is that $\Theta = \theta$ when the observation $X$ was made.

By contrast, in Classical Inference, the unknown quantity $\theta$ is viewed as a deterministic constant that happens to be unknown. It then strives to develop an estimate of $\theta$ that has some performance guarantees.

Suppose that we are trying to measure a physical constant, say the mass of the electron, by means of noisy experiments. The classical statistician will argue that the mass of the electron, while unknown, is just a constant, and that there is no justification for modeling it as a random variable. The Bayesian statistician will counter that a prior distribution simply reflects our state of knowledge. For example, if we already know from past experiments a rough range for this quantity, we can express this knowledge by postulating a prior distribution which is concentrated over that range.

A classical statistician will often object to the arbitrariness of picking a particular prior. A Bayesian statistician will counter that every statistical procedure contains some hidden choices. Furthermore, in some cases, classical methods turn out to be equivalent to Bayesian ones, for a particular choice of a prior. By locating all of the assumptions in one place, in the form of a prior, the Bayesian statistician contends that these assumptions are brought to the surface and are amenable to scrutiny.