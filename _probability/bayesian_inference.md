---
layout: default
title: Bayesian Inference
slug: bayesian
item_num: 7
excerpt: Statistical Inference is the process of extracting information about an unknown variable or an unknown model from available data. The Bayesian approach essentially tries to move the field of statistics back to the realm of probability theory. The unknown variables are treated as random variables with known prior distrubtions.
---

$$
\newcommand{\expect}{\mathrm{E}}
\newcommand{\prob}{\mathrm{P}}
\newcommand{\v}{\mathrm{var}}
\newcommand{\Comb}[2]{ {}^{#1}C_{#2} }
$$

# Bayesian Inference

## Pre-requisites

For understanding statistical inference, you need to be familiar with the following concepts:
* Basics of Probability (including Random Variables, PMFs, PDFs, CDFs, Conditional Probabilities, Expectations, Variances, etc.)

* **The Sum Rule** : The marginal probability is the sum over all joint probabiliites.

$$
p_X(x) = \sum_{y} p_{X, Y}(x,y)
$$

* **The Product Rule** : 

$$
p_{X, Y}(x, y) = p_X(x)p_{Y\mid X}(y \mid x)
$$

* Normal Distributions

Knowledge of the Limit Theorems is also good to have. These laws provide a mathematical basis for the loose interpretation of the expected value $\expect[X]$ as the average of a large number of independent samples drawn from the distribution of $X$. Limit Theorems are useful for several reasons:

1. Conceptually, they provide an interpretation of Expectation (as well as Probability) in terms of a long sequence of identical independent experiments.
2. They allow us to derive an approximate probability distribution for the sum $S_n$ of large number of i.i.d random variables $X_1,X_2,\dots,X_n$.
3. They play a major role in *classical* inference, in the presence of large data sets.



## Statistical Inference

Statistical Inference is the process of extracting information about an unknown variable or an unknown model from available data. Statistics generally involves an element of art. For any particular problem, there may be several reasonable methods, yielding different answers. There is no principled way for selecting the "best" method, unless one makes several assumptions and imposes additional constraints on the inference problem.

Within the field of statistics there are two prominent schools of thought, with opposing views: the Bayesian and the Classical (also called Frequentist). Their fundamental difference relates to the nature of the unknown models or variables. In the Bayesian view, they are treated as random variables with known distributions. In the classical view, they are treated as deterministic quantities that happen to be unknown.

The Bayesian approach essentially tries to move the field of statistics back to the realm of probability theory. The unknown variables are treated as random variables with known prior distrubtions. We conduct an experiment, make some observation ($X$) and then try to infer the value of the random variable ($\Theta$) during the conducted experiment. We derive a posterior distribution $\prob(\Theta \mid X)$ which tells us how likely it is that $\Theta = \theta$ when the observation $X$ was made.

By contrast, in Classical Inference, the unknown quantity $\theta$ is viewed as a deterministic constant that happens to be unknown. It then strives to develop an estimate of $\theta$ that has some performance guarantees (confidence interval).

Suppose that we are trying to measure a physical constant, say the mass of the electron, by means of noisy experiments. The classical statistician will argue that the mass of the electron, while unknown, is just a constant, and that there is no justification for modeling it as a random variable. The Bayesian statistician will counter that a prior distribution simply reflects our state of knowledge. For example, if we already know from past experiments a rough range for this quantity, we can express this knowledge by postulating a prior distribution which is concentrated over that range.

A classical statistician will often object to the arbitrariness of picking a particular prior. A Bayesian statistician will counter that every statistical procedure contains some hidden choices. Furthermore, in some cases, classical methods turn out to be equivalent to Bayesian ones, for a particular choice of a prior. By locating all of the assumptions in one place, in the form of a prior, the Bayesian statistician contends that these assumptions are brought to the surface and are amenable to scrutiny.

### Types of Inference Problems

In **parameter estimation**, we want to generate estimates that are close to the true values of the parameters in some probabilistic sense. In this kind of problem, a model (likelihood distribution) is fully specified, except for an unknown, possibly multidimensional, parameter $\theta$, which we wish to estimate. This parameter can be viewed as either a random variable (Bayesian approach) or as an unknown constant (Classical approach). The usual objective is to arrive at an estimate of $\theta$ that is close to the true value in some sense. For example, using polling data, estimate the fraction of a voter population that prefers candidate A over candidate B.

In a **binary hypothesis testing** problem, we start with two hypotheses and use the available data to decide which of the two is true. For example, the Airplane-Radar example discussed earlier, where we have to infer whether an airplane was present or not, given the radar reading.



## Intro to Bayesian Inference
*Lecture 14*

Here, we study the Bayes’ Rule in detail. We learn how to calculate the Posterior distribution and how to summarize the distribution using one number: either the most probable value (where posterior is highest) or the expected value (mean value).  

### Bayesian Framework

In Bayesian Framework, the unknown quantity is modelled as a random variable, denoted by $\Theta$. It has a prior distribution $\prob_\Theta$. We aim to extract information about $\Theta$, based on another random variable observed during the experiment $X=(X_1, X_2, \dots, X_n)$. This random variable is called **observation, measurement** or an **observation vector**.

Based on $X$, we try to guess the value that $\Theta$ took during the experiment. For this we are given a model $\prob(X \mid \Theta)$. Once we have made an observation, we make a judgement about $\Theta$ by calculating posterior distribution $\prob(\Theta \mid X)$ using Bayes' Rule.

$P(\Theta \mid X)$ is called the **Posterior Distribution** because here we have already made the observation and we are trying to go back and guess what value the random variable $\Theta$ took.  

$P(X \mid \Theta)$ is called the **Likelihood Distribution** because it tells us how likely $X$ is to take a value $x$ (likelihood of data), given the value of $\Theta$.  

$P(\Theta)$ is called the **Prior Distribution**, because it gives the probability of $\Theta = \theta$ before any observation is made. The prior comes from symmetry, known range, earlier studies, subjectivity etc.

Below is a list of the four different possible scenarios between continuous/discrete $\Theta$ and continuous/discrete $X$.

![Bayes Rule](/assets/images/probability/bayesian_inference.assets/image-20200702012847994.png)

Let us look at a particular example where unknown is continuous and observation is discrete. We want to find the posterior probability of bias (probability of heads) of a coin, given the number of heads ($k$) in $n$ coin tosses. The formula for the posterior distribution is given above (continuous $\Theta$, discrete $X$ scenario). The prior $f_\Theta(\theta)$ is uniform over the interval $[0,1]$.  

$$
\begin{align}
p_{K | \Theta}(k | \theta) &= \Comb{n}{k} \theta^k (1-\theta)^{n-k} \\
f_{\Theta | K}(\theta | k) &= \frac{1 \cdot \Comb{n}{k} \theta^k (1-\theta)^{n-k}}{p_{K}(k)} \\
&= \frac{1}{d(n,k)} \theta^k (1-\theta)^{n-k} \\
\end{align}
$$

$d(n,k)$ is the Normalizing Constant (doesn't vary with $\Theta$). The distribution given by the above formula is called **Beta distribution** with parameters $(k+1, n-k +1)$. Notice that if we start with a Prior that is a Beta Distribution, then the Posterior still belongs to the Beta family. Priors of this sort are known as Conjugate Priors.  

### Point Estimates

Many a times we are not interested in the posterior distribution of $\Theta$ over its entire range. We just need a point estimate for $\Theta$ given the value of $X$. Given a value of $X$ (say $x$), the point estimator takes a specific value based on the function $\prob(\Theta \mid X = x)$, . Therefore, the point estimator itself is a random variable denoted by $\hat{\Theta}$. Any value that the point estimator takes is called an estimate and is denoted by $\hat{\theta}$.

The value of $\hat{\theta}$ is to be determined by applying some function $g$ to the observation $x$, resulting in $\hat{\theta} = g(x)$. The random variable $\hat{\Theta} = g(X)$ is called an estimator, and its realized value equals $g(x)$ whenever the random variable $X$ takes the value $x$. As explained, the reason that $\hat{\Theta}$ is a random variable is that the outcome of the estimation procedure depends on the random value of the observation.

We can use different functions $g$ to form different estimators; some will be better than others. For an extreme example, consider the function that satisfies $g(x) = 0$ for all $x$. The resulting estimator, $\hat{\Theta} = 0$, makes no use of the data, and is therefore not a good choice. We study two of the most popular estimators: 

**Maximum a Posteriori Probability (MAP) Estimator**

![MAP Rule for Estimation](/assets/images/probability/bayesian_inference.assets/image-20200702013916791.png)

**Conditional Expectation Estimator**

$$
\hat{\theta} = \expect[\Theta \mid X=x]
$$

It is also called the least mean squares (LMS) estimator because it has an important property: it minimizes the Mean Squared Error over all estimators.

$$
\begin{align}
\expect[(\Theta - \hat{\theta})^2] &= \v(\Theta - \hat{\theta}) + (\expect[\Theta - \hat{\theta}])^2 \\
 &= \v(\Theta) + (\expect[\Theta - \hat{\theta}])^2 \\
 &= \v(\Theta) + (\expect[\Theta] - \hat{\theta}])^2 \\
\end{align}
$$

The above quantity is minimized when $\hat{\theta} = \expect[\Theta]$. If we substitute general probabilities with posterior probabilities, then the error minimizer is 

$$
\hat{\theta} = \expect[\Theta \mid X]
$$

If the posterior distribution is symmetric around its (conditional) mean and unimodal (i.e., has a single maximum), the maximum occurs at the mean. Then, the MAP estimator coincides with the conditional expectation estimator.

### Hypothesis Testing

In a hypothesis testing problem, $\Theta$ takes one of $m$ values, $\theta_1,\theta_2,\dots,\theta_m$, where m is usually a small integer; often $m = 2$, in which case we are dealing with a binary hypothesis testing problem. We refer to the event ${\Theta = \theta_i}$, as the $i$th hypothesis and denote it by $H_i$.

![MAP Rule for Hypothesis Testing](/assets/images/probability/bayesian_inference.assets/image-20200702013747166.png)

Watch this [video](https://www.youtube.com/watch?v=_hDfZF64wic) for a nice summary of all the topics discussed in Lecture 14.



## Linear Models with Normal Noise

*Lecture 15*

Here we study the continuous unknown, continuous observation case of Bayesian inference. We consider a specific case where the unknown variables and noise variables are all independent normals. Further,

$$
X = W + \Theta
$$

where $X$ is the observation variable, $W$ is the noise variable and $\Theta$ is the unknown variable (to be inferred). $X$ is a linear function of independent normal variables $W$ and $\Theta$. Hence, $X$ is itself a normal variable.

### Recognizing Normal Distribution

![normal_fn](/assets/images/probability/bayesian_inference.assets/normal_fn.png)

All functions of the above form are normal distributions. You don’t really need to remember the mean and variance. Comparing the above equation with $f(x) = \frac{1}{\sigma\sqrt{2\pi}}e^{\frac{-(x-\mu)^2}{2\sigma^2}}$, we know that coefficient of $x^2 = \frac{1}{2\sigma^2} = \alpha$. Also, the mean is where the function takes the biggest value. That is the point where the absolute value of exponent of e takes the smallest value. Differentiating the exponent function you get the mean.

The above formulation also tells us that product of normal probabilities is also normal.  

### Estimating Normal RV in Normal Noise

**Single Unknown, Single Observation**

In our experiment, $X = W + \Theta$, where $X$ is the observation variable, $W$ is the noise variable and $\Theta$ is the unknown variable (to be inferred). The assumption that we make is that $\Theta$ and $W$ are normal variables. To simplify the calculations we will take them to be standard normal variables that are independent of each other. Inference about $\Theta$ is basically a calculation of the posterior distribution of $\Theta$, denoted by $f_{\Theta \mid X}(\theta \mid x)$. To find the posterior distribution of $\Theta$, we need to calculate the likelihood of observation.

$$
\begin{align}
f_{X | \Theta}(x | \theta) &= N(\theta, 1) &\textrm{bcoz }
X = \theta + W
\end{align}
$$

Because prior and likelihood are both normal distribution, the posterior distribution is also normal (product of normal distributions). Therefore we can say that:

$$
\hat{\theta}_{LMS} = \hat{\theta}_{MAP} = \expect[\Theta \mid X = x]
$$

By writing out the posterior as the product of prior ($N(0, 1)$) and likelihood ($N(\theta, 1)$), and taking the derivative of its exponent term, we can find the peak of this normal distribution. We get the following result:

$$
\hat{\theta}_{LMS} = \hat{\theta}_{MAP} = \expect[\Theta \mid X = x] = x/2 
$$

In terms of random variables, this can be written as

$$
\hat{\Theta}_{LMS} = \hat{\Theta}_{MAP} = \expect[\Theta \mid X] = X/2
$$

Even for the case where $\Theta$ and $W$ are independent normal random variables, but with general means and variances, we can prove that:

- posterior is still normal,
- LMS and MAP estimators coincide,
- the estimators are a linear function of the observation $X$, given as $\hat{\Theta} = aX + b$.

**Single Unknown, Multiple Observations**

Here $X$ is an n-dimensional vector as we make multiple observations $X_1, X_2, \dots, X_n$. All the observations are made at one particular value of $\Theta$. Therefore,

$$
X_1 = \Theta + W_1 \\
X_2 = \Theta + W_2 \\
\vdots\\
X_n = \Theta + W_n \\
\textrm{where, } W_i \sim N(0,\sigma_i^2) \textrm{ and } \Theta \sim N(x_0, \sigma_0^2)\\
\textrm{ and } \Theta, W_1, \dots, W_n \textrm{ are all independent}
$$

The noise in each observation is different, but the value of the underlying unknown is the same. Though $\Theta$ can take different values, when we conduct the experiment we record observations $x_1, \dots, x_n$ for some particular value $\theta$ and now we are trying to estimate that value using the posterior distribution.  

How do we find $f_{X_i \mid \Theta}(x_i \mid \theta)$? If it is given that $\Theta = \theta$, then we know that $X_i = \theta + W_i \sim N(\theta, \sigma_i^2)$. Thus,

$$
f_{X_i | \Theta}(x_i \mid \theta) = c_i \textrm{exp}\bigg(-\frac{(x_i - \theta)^2}{2\sigma_i^2}\bigg)
$$

Also, all $X_i$(s) are indepedent of each other and of $\Theta$. Therefore,

$$
f_{X | \Theta}(x | \theta) = f_{X_1, \dots ,X_n \mid \Theta}(x_1,\dots, x_n\mid \theta) =\prod_{i =1}^n f_{X_i \mid \Theta}(x_i, \theta)
$$

Using the Bayes' Rule we can now obtain the posterior distribution $f_{\Theta \mid X}$ (by multiplying the above mentioned likelihood with the prior over $\Theta$). Because this distirbution is also a normal distribution, the peak coincides with the mean.  Again to obtain the MAP Estimator, we differentiate the quadratic exponent of the posterior distribution w.r.t. $\theta$.

$$
\hat{\theta}_{LMS} = \hat{\theta}_{MAP} = E[\Theta \mid X=x] = \frac{\sum_{i=0}^{n}\frac{x_i}{\sigma_i^2}}{\sum_{i=0}^{n}\frac{1}{\sigma_i^2}}
$$

We can see here that the estimate is a weighted average of all the $x_i$(s), weights being inverse of the variance. This makes sense intuitively, because if $\sigma_i^2$ is large, then the noise $W_i$ is large and $X_i$ should be given less weight as compared to the less noisy observations. Also, notice that $x_1, \dots, x_n$ represent the observations but $x_0$ represents the prior mean. We combine the value of the observations with the value of the prior mean. In some sense, the prior mean is treated as just one more piece of information (one more observation).

**Multiple Unknowns, Multiple Observations**

In this model, $X$ and $\Theta$ are both  multi-dimensional vectors. We study this case using the Trajectory Example. We know that the trajectory of a projectile is parabolic with time. Therefore, the relation between observations (height measurements) $X_i$(s), and time $t_i$ is given as follows:

$$
X_i = \Theta_0 + \Theta_1t_i + \Theta_2t_i^2 + W_i
$$

Here $W_i$ represents the noise introduced by our measuring instrument. $\Theta_j$(s) are the unknown parameters that we have set out to discover. In our particular example, $\Theta_0$ gives the (initial) height, $\Theta_1$ gives the (initial) speed and $\Theta_2$ gives the acceleration. All these variables can take any value during an experiment. We would have a prior distribution of these values based on the average height of buildings in an area, the velocity with which people can throw a ball vertically, gravitational acceleration etc. We will assume that $\Theta_j$(s) and $W_i$(s) are independent of each other. From how measuring devices work in real-world, this assumption is pretty realistic.

We will also assume the following

$$
\Theta_j \sim N(0, \sigma_j^2)\\ 
W_i \sim N(0, \sigma^2)
$$

We would now like to estimate the parameters $\Theta_j$(s) based on our observations $X_i$(s). But before that let us try to understand better what we are trying to achieve here.  

From the main equation above, we know that $f_{X_i \mid \Theta} \sim N(\theta_0 + \theta_1t_i + \theta_2t_i^2, \sigma)$. To increase the likelihood of observations, the observations need to be as close to the estimated trajectory (given by $\theta_0 + \theta_1t_i + \theta_2t_i^2$) as possible. During MAP estimation, we try to estimate an unknown variable so that the likelihood of observations is high while also keeping the unknown variable close to its prior distribution. Thus, our aim here is to come up with a $\hat{\Theta}$, such that the estimated trajectory is close to the observations, while keeping the estimate reasonably close to its prior distribution.  


A key difference between the Trajectory Problem and "Single Unknown, Multiple Observations" scenario is that here all the $X_i$(s) are not identically distributed. In the previous scenario $f_{X_i \mid \Theta}$ was the same for all $i$(s). Here the mean for all such $f_{X_i \mid \Theta}$ is different, and depends on the time of the observation. 

We will, as usual, use the appropriate form of Bayes' Rule to find the posterior distribution of unknown parameters.

$$
f_{\Theta \mid X} = f_{X \mid \Theta}  f_{\Theta} = f_{\Theta} f_{X_1 \mid \Theta} f_{X_2 \mid \Theta} \dots = \prod_{j = 1}^{3}f_{\Theta_j}\prod_{i = 1}^n f_{X_i \mid \Theta}
$$

In the above derivation we have used the fact that given a particular value of $\Theta$, all the $X_i$(s) are independent, because all the noise terms $W_i$(s) are independent. Thus $f_{X \mid \Theta} = \prod_{i = 1}^n f_{X_i \mid \Theta}$.

We observe that the posterior distribution is a normal function (product of multiple normal distributions). To get the MAP estimate (same as LMS) we need to find the peak of the normal curve. We do this by taking partial derivates with respect to $\theta_0, \theta_1, \theta_2$ and equating them to $0$. Thus we have three equations and three unknowns.  

The Trajectory Estimation Problem gives a glimpse into a large field that deals with **Linear Normal Models**. Here, for each problem we assume the existence of some underlying independent normal random variables and the observations $X_i$ and the unknown parameters $\Theta_j$ are linear functions of these underlying variables. $X_i$ and $\Theta_j$ are also normal, because linear functions of independent normal variables are normal too. Problems of this kind occur very frequently in practice. The Posterior is always of the form :

$$
 f_{\Theta | X}(\theta | x) = c(x)\mathrm{exp\{-quadratic(\theta_1,\theta_2,\dots)\}}
$$

MAP estimate maximizes the posterior over $(\theta_1, \theta_2, \dots)$ and thus minimizes the quadratic function in the exponent. Equating the partial derivates (with respect to $\theta_1, \theta_2, \dots$) to zero gives us a system of linear equations. As we saw in the examples above

$$
\hat{\Theta}_{MAP,j} : \textrm{Linear Function of }X = (X_1, \dots, X_n)
$$


Therefore, carrying out inference under this model is given the name **linear regression**. Inference (MAP estimation) under Linear Normal Model is the same as finding the parameters of the curve, such that the distance between the curve and the points (observations) is as less as possible. Refer to Section 9.2 of *Introduction to Probability.* 2nd ed. (Bertsekas, Dimitri, and John Tsitsiklis) for a more systematic analysis of Linear Regression using both Bayesian and Classical Inference.


## Least Mean Squares Estimation

*Lecture 16*

So far we've seen two ways of estimating a parameter : maximum aposteriori estimation and conditional expectation. These were arbitrary choices. Here we will first decide upon a performance criterion and then find an estimator that is optimal with respect to that criterion. Our criterion will be the expected value of squared estimation error. It will turn out that the Conditional Expectation is the optimal estimator for this criterion. That is why we've been calling it Least Mean Squares Estimator all along.

### Warm Up

Let us first consider the case where we don't have any observation. Therefore we are trying to estimate $\Theta$ based on the prior distribution (the posterior is the same as the prior). Let us say the prior distibution is uniform in the interval $[4, 10]$. In this case, the MAP and Conditional Expectation estimators are given as follows:

- MAP Rule : $\hat{\theta} \in [4, 10]$

* Conditional Expectation : $\hat{\theta} = 7$

Instead of picking an estimator according to some arbitrary rule, let us find an estimator according to the following criterion:

$$
\hat{\theta} = \textrm{arg}\min_{\hat{\theta}} \expect[(\Theta - \hat{\theta})^2]
$$

The expected value of $\Theta$ is the optimal estimator according to this criterion. Proof?

$$
\begin{align}
\expect[(\Theta - \hat{\theta})^2] &= \v(\Theta - \hat{\theta}) + (\expect[\Theta - \hat{\theta}])^2 \\
&= \v(\Theta) + (\expect[\Theta] - \hat{\theta})^2  &\hat{\theta}\textrm{ is a constant}
\end{align}
$$

We can't reduce the variance of the random variable $\Theta$. We can only reduce the second term by setting $\hat{\theta} = \expect[\Theta]$.

### Estimation with Observation

Here again we want to find a point estimate $\hat{\theta}$ for the unknown variable $\Theta$ with prior $\prob_{\Theta}(\theta)$. But in this case, we also have an observation $X = x$. In the warm-up example, we wanted a point estimate that would minimize the squared estimation error, given by $\expect[(\Theta - \hat{\theta})^2]$. Here we would want to minimize the conditional mean squared error given by

$$
\expect[(\Theta -\hat{\theta})^2 \mid X = x]
$$

As in the warm-up example, the solution is given by the expected value of $\Theta$, but now in the conditional universe.

$$
\hat{\theta} = \expect[\Theta \mid X = x]
$$

![LMS Estimation](/assets/images/probability/bayesian_inference.assets/image-20200703135229153.png)

### Performance of the LMS Estimator

Given an observation $X=x$, we know that the optimal estimator for minimizing the criterion $\expect[(\Theta -\hat{\theta})^2 \mid X = x]$ is given by $\expect[\Theta \mid X =x ]$. We haven't explicitly talked about the performance of our estimator with respect to our chosen criterion. 

Expected performance when we already have a measurement:

$$
\textrm{MSE} = \expect[(\Theta -\expect[\Theta \mid X = x])^2 \mid X = x] = \v(\Theta \mid X = x)
$$


What is the expected performance over all possible values of $X$? In this case the estimator is given as $\hat{\Theta} = \expect[\Theta \mid X]$

$$
\begin{align}
\textrm{MSE} &= \expect[(\Theta - \hat\Theta)^2] \\
&= \expect[\expect[(\Theta -\hat{\Theta})^2 \mid X]] &\textrm{Law of Iterated Expectations} \\
&= \expect[\v(\Theta \mid X)] &\textrm{Proved Above} \\
\end{align}
$$

### Challenges

What if we have multiple observations? In this case the estimator will still be of a similar form:

$$
\hat{\Theta} = \expect[\Theta \mid X_1 = x_1, \dots, X_n = x_n]
$$

What if we have multiple observations and multiple unknown variables? In this case $X = (X_1, X_2, \dots, X_n)$ and $\Theta = (\Theta_1, \Theta_2, \dots, \Theta_n)$. In this case we can get the expected value of each unknown variable individually, as follows:  

$$
\hat{\Theta}_j = \expect[\Theta_j\mid X_1 = x_1, \dots , X_n = x_n]
$$

However, it is not always this easy to compute/analyze the LMS estimator. Why?

We have to first find out the distribution $f_{\Theta \mid X}$ (before finding out the conditional expectation). We do this using Bayes' Rule. This can be terribly hard to obtain because of the following reasons:

* Many a times we don't know the correct model for $f_{X \mid \Theta}$ especially when $X$ and $\Theta$ are multi-dimensional.
* Even if you have the correct likelihood model, $f_X$ (the probability of data) is tremendously hard to obtain (theoretically and practically).
* Finally, even if you can get your hands on the posterior of $\Theta$ ( $f_{\Theta \mid X}$ ), the conditional expectation of $\Theta_j$ will require a multi-dimensional integral.

$$
\expect[\Theta_j \mid X = x] = \int\Theta_jf_{\Theta \mid X}d\Theta = \int\int\int\Theta_jf_{\Theta \mid X}d\Theta_1d\Theta_2d\Theta_3\dots
$$

This is why we will look at other estimation techniques, that will be significantly easier to compute.



## Linear Least Mean Square Estimation

*Lecture 17*

If our sole aim is to keep the mean squared error small, then the conditional expectation is the best estimator. But as mentioned before, the conditional expectation can be tremendously difficult to compute. Maybe we are missing some of the needed distributions, or maybe we have all the distributions, but they are very complicated and cumbersome for expectation calculation. Here, we will consider an estimator that has a simpler structure, an estimator that is a linear combination of the observations. Thus, we will derive an estimator that minimizes the mean squared error within a restricted class of estimators (known as hypothesis set): those that are linear functions of the observations. While this estimator may result in higher mean squared error, it has a significant practical advantage: it requires simple calculations, involving only means, variances. and covariances of the parameters and observations. It is thus a useful alternative to the conditional expectation in cases where the latter is hard to compute.

A linear estimator of a random variable $\Theta$, based on observations $X_1 , \dots , X_n$, has the form

$$
\hat{\Theta} = a_1X_1 + \dots + a_nX_n + b
$$

Given a particular choice of the scalars $a_1, \dots , a_n, b$ the corresponding mean squared error is

$$
\expect[(\Theta - a_1X_l - \dots - a_nX_n - b)^2]
$$

In cases, where the conditional expectation itself is linear in the observations, the best linear estimation will be the conditional expectation itself, and

$$
\hat{\Theta}_{LLMS} = \hat{\Theta}_{LMS} = \expect[\Theta \mid X] = a_1 X_1 +\dots+a_nX_n + b
$$

### Single Observation

The estimator is of the form:

$$
\hat{\Theta} = aX + b
$$

We are interested in finding $a$ and $b$ that minimize the mean squared estimation error $E[(\Theta - aX -b)^2]$. Suppose that $a$ has already been chosen. How should we choose $b$? This is the same as choosing a constant $b$ to estimate the random variable $\Theta - aX$. The best choice is $b = E[\Theta - aX] = E[\Theta] - aE[X]$.

![image-20200703160457603](/assets/images/probability/bayesian_inference.assets/image-20200703160457603.png)

The formula for the linear LMS estimator only involves the means, variances, and covariance of $\Theta$ and $X$. Furthermore, it has an intuitive interpretation. The estimator starts with the baseline estimate $\expect[\Theta]$, which it then adjusts by taking into account the value of $X - \expect[X]$. Suppose $\textrm{cov}(\Theta, X)$ is positive. This means that the estimator should increase in proportion to $X - \expect[X]$. The LLMS estimator equation shows that the proportionality constant is $a = \frac{\textrm{cov}(\Theta, X)}{\v(X)}$. If $\rho = 0$, then $X$ and $\Theta$ are not correlated, so a given value of $X$ should not affect the value of the estimator for $\Theta$.

### Multiple Observations

In this case $\Theta$ is the unknown and $X = (X_1, \dots, X_n)$ are the observations. Our estimator is of the form $\hat{\Theta} = a_1 X_1 + \dots + a_n X_n + b$ and we have to find value $a_1, \dots, a_n, b$ such that the mean square error of estimation is the lowest (amongst all linear estimators), i.e.

$$
\textrm{minimize: } \expect[(a_1 X_1 + \dots + a_n X_n + b - \Theta)^2]
$$

When we expand the equation above (using linearity of expectations) and take derivatives with respect to $a_1, \dots, a_n, b$, we get a system of linear equations in $a_i$(s) and $b$. The good part about this is that the solution only depends on the means, variances and covariances of the observations and unknown parameters. We don't need to know or deal with full probability distributions. 

### Linear Estimation and Normal Models

The linear LMS estimator is generally different from and, therefore, inferior to the LMS estimator $\expect[\Theta \mid X_1, \dots, X_n]$. However, if the LMS estimator happens to be linear in the observations $X_1 , \dots, X_n$, then it is also the linear LMS estimator, i.e. the two estimators coincide.

An important example where this occurs is the estimation of a normal ran­dom variable $\Theta$ on the basis of observations $X_i = \Theta + W_i$, where the $W_i$ are independent zero mean normal noise terms, indepedent of $\Theta$. We have seen this example in Lecture 15 (section on inference with single unknown and multiple observations), where we found that the conditional expectation, $\expect[\Theta \mid X = (x_1, \dots, x_n)]$, is linear in the observations (average of the observations, weighted by the inverse of the variance of the observation). If we calculate the Linear LMS Estimator using the technique mentioned above, we get the same estimator. Thus, the LMS and the linear LMS estimators coincide. This is a manifestation of a property that can be shown to hold more generally: if $\Theta, X_1, \dots, X_n$ are all linear functions of a collection of independent normal variables, then the LMS and Linear LMS estimators coincide. They also coincide with the MAP estimator, since the normal distribution is symmetric and unimodal.

The above discussion leads to an interesting interpretation of linear LMS estimation: the estimator is the same as the one that would have been obtained if we were to pretend that the random variables involved were normal, with the given means, variances, and covariances. Thus, there are two alternative perspectives on linear LMS estimation: either as a computational shortcut (avoid the evaluation of a possibly complicated formula for $\expect[\Theta \mid X]$), or as a model simplification (replace less tractable distributions by normal ones).
