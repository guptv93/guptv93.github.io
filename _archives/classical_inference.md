---
layout: default
title: Classical Inference
slug: frequentist
item_num: 8
excerpt: In Bayesian view, the unknown variables are treated as random variables with known prior distrubtions. By contrast, in Classical Inference, the unknown quantity $\theta$ is viewed as a deterministic constant that happens to be unknown. It then strives to develop an estimate of $\theta$ that has some performance guarantees.
---


$$
\newcommand{\expect}{\mathrm{E}}
\newcommand{\prob}{\mathrm{P}}
\newcommand{\v}{\mathrm{var}}
\newcommand{\Comb}[2]{ {}^{#1}C_{#2} }
$$

# Classical Inference


## Bayesian vs Frequentist

Within the field of statistics there are two prominent schools of thought, with opposing views: the **Bayesian** and the **Classical** (aka **Frequentist**). 

In Bayesian view, the unknown variables are treated as random variables with known prior distrubtions. We conduct an experiment, make some observation $X$, and then try to infer the value of the random variable $\Theta$ during the conducted experiment. We derive a posterior distribution $P(\Theta \mid X)$ which tells us how likely it is that $\Theta = \theta$ when the observation $X$ was made.

By contrast, in Classical Inference, the unknown quantity $\theta$ is viewed as a deterministic constant that happens to be unknown. It then strives to develop an estimate of $\theta$ that has some performance guarantees (confidence interval). Suppose that we are trying to measure a physical constant, say the mass of the electron, by means of noisy experiments. The classical statistician will argue that the mass of the electron, while unknown, is just a constant, and that there is no justification for modeling it as a random variable. The Bayesian statistician will counter that a prior distribution simply reflects our state of knowledge. For example, if we already know from past experiments a rough range for this quantity, we can express this knowledge by postulating a prior distribution which is concentrated over that range. 

A classical statistician will often object to the arbitrariness of picking a particular prior. A Bayesian statistician will counter that every statistical procedure contains some hidden choices. Furthermore, in some cases, classical methods turn out to be equivalent to Bayesian ones, for a particular choice of a prior. By locating all of the assumptions in one place, in the form of a prior, the Bayesian statistician contends that these assumptions are brought to the surface and are amenable to scrutiny.




## Classical Inference

In classical inference we treat the unknown parameter as an unknown constant ($\theta$) rather than a random variable ($\Theta$). The observation $X = (X_1, X_2, \dots, X_n)$ is a random variable, whose probability distribution depends on the value of $\theta$. This probability distribution is denoted by $p_X(x;\theta)$. Remember that this indicates that $p_X$ is dependent on $\theta$, not that it is conditioned on $\theta$ in the probablistic sense.

**$\theta$ is not a random variable. It just decides the probabilities of other random variables, like $X$.**  

![Classical Inference](/assets/images/probability/classical_inference.assets/image-20200704112537755.png)

Our task in classical inference is to come up with an estimate $\hat{\Theta}$. The estimate is decided on the basis of the observations $X$ made during the experiment. Thus $\hat{\Theta} = g(X)$. Recall that a function of a random variable is a random variable itself. Thus $\hat{\Theta}$ is also a random variable. Each time we conduct the experiment,  $X$ takes the value $x$ and $\hat{\Theta}$ takes a value $\hat{\theta}$. $g$ is called the estimator function, and the process of designing the estimator is called modelling. The model should be such that it gives a **"close enough"** estimate of $\theta$ for all possible values of $\theta$.


There are two types of tasks in classical inference:
1. Parameter Estimation:
    
	In parameter estimation, $\theta$ can take values from a continuous range of real numbers. Thus, we have to assign a value to $\hat{\Theta}$ from this continuous interval.  We are interested in estimators ($g$) that have some desirable properties. For example, we may require that the expected value of the estimation error be zero, or that the estimation error be small with high probability, for all possible values of $\theta$.
    
2. Hypothesis Testing:

    In hypothesis testing, there are only a fixed number of discrete values that $\theta$ can take and we have to choose a value (from all possible values) for $\hat{\Theta}$ in each experiment. In particular, $g$ calculates the "likelihood" of each hypothesis under the observed data, and chooses a hypothesis by comparing the likelihoods with a suitably chosen threshold. Here the range of $g$ is the set of all possible hypothesis.



## Parameter Estimation

### Expected Value Estimation

We will study Classical Estimation by trying to estimate the mean of a random variable. Suppose $X_1,X_2,\dots,X_n$ are i.i.d. (independent identically distributed) random variables drawn from a Gaussian Distribution with mean $\theta$ and variance $\sigma^2$. Parameter $\theta$ is unknown and we want to estimate it using classical statistics.

We can take our estimator to be $g$, where

$$
\hat\Theta_n = g((X_1, X_2, \dots, X_n)) = \textrm{sample mean} = \frac{X_1 + X_2 + \dots + X_n}{n}
$$

The desirable properties of any estimator $g$ are as follows:  
1. $\expect[\hat\Theta_n] = \theta$ **(zero bias)**  
	This property should be true for all $\theta$. We don't want our estimates to be systematically low or high, no matter what the value of $\theta$ is. This property is true for our estimator function above.

2. $\hat\Theta_n \to \theta$, as $n \to \infty$ **(consistency)**  
	This property also should be true for all $\theta$. Weak Law of Large Numbers ensures that our simple estimator for mean estimation problem above, follows this property for all values of $\theta$.

3. Mean Squared Error $\expect[(\hat\Theta_n - \theta)^2]$ **(mse)**  
	Mean squared error should be as less as possible. For our specific problem of mean estimation and our specific estimator $g$, we know that $\expect[\hat\Theta_n] = \theta$. Therefore, $E[(\hat\Theta_n - \theta)^2] = \v(\hat\Theta_n) = \sigma^2/n$. Therefore, as $n$ increases, the value of MSE decreases.


### Mean Squared Error of an Estimator

Unlike the example that we saw above, $\expect[\hat\Theta_n] \neq \theta$ for all estimation problems. In that case, using the identity $\expect[Z^2] = \v(Z) + (\expect[Z])^2$, we derive:  

$$
\expect[(\hat{\Theta} - \theta)^2] = \v(\hat{\Theta} - \theta) + (\expect[\hat{\Theta} - \theta])^2 = \v(\hat{\Theta}) + (\expect[\hat{\Theta}] - \theta)^2 = \v(\hat{\Theta}) + \textrm{bias}^2
$$

In the previous example, our bias was zero. So,

$$
\expect[(\hat\Theta_n - \theta)^2] = \v(\hat\Theta_n) = \sigma^2/n
$$

If we take a dumb estimator which always gives out an estimate of 0, irrespective of the observation, then

$$
\expect[(\hat\Theta_n - \theta)^2] = \v(\hat\Theta_n) + \textrm{bias} = 0 + (0 - \theta)^2 = \theta^2
$$

Generally, the task of Parameter Estimation includes reporting the $MSE$ or $\sqrt{MSE}$, along with designing and implementing an estimator with most of the desirable properties.

### Confidence Interval

The value of an estimator $\hat{\Theta}$ may not be informative enough on its own. One common practice is to provide the standard error along with the estimate. Another technique is to specify a confidence interval.

To find a $1 - \alpha$ confidence interval, we replace the point estimator $\hat\Theta_n$ by a lower estimator $\hat\Theta_-$, and an upper estimator $\hat\Theta_+$, such that

$$
\begin{align}
\prob(\hat{\Theta}_- \leq \theta \leq \hat{\Theta}_+) \geq 1-\alpha && \forall \theta
\end{align}
$$

$\alpha$ mostly takes a value of $0.05$ or $0.01$. 

We have mentioned beforhand that $\theta$ is not a random variable. Then how does probability of $\theta$ lying in an interval make sense? It makes sense because $\hat\Theta_-$ and $\hat\Theta_+$ are random variables. The probability is the likelihood of our range being correct, not the likelihood of $\theta$ taking up a particular value. Suppose that after the observations are obtained, the confidence interval turns out to be $[-2.3,4.1]$. We cannot say that $\theta$ lies in $[-2.3, 4.1]$ with probability $0.95$, because the latter statement does not involve any random variables; after all, in the classical approach, $\theta$ is a constant.

For a concrete interpretation, look at it like this. We construct a confidence interval many times, using the same statistical procedure, i.e., each time, we obtain an independent collection of $n$ observations, and construct the corresponding $95$% confidence interval. We then expect that about $95\%$ of these confidence intervals will include $\theta$. This would be true regardless of what the value of $\theta$ is. A much better way to explain confidence intervals is through the Mean Estimation Problem below.

**Confidence Interval for the Mean Estimation Problem:**

Suppose that the observations $X_i$ are i.i.d. normal, with unknown $\theta$ and known variance $\sigma^2$. We want to find a $95\%$ confidence interval for $\theta$. Then the sample mean estimator 

$$
\hat\Theta_n = \frac{X_1 + \dots + X_n}{n}
$$

is normal, with mean $\theta$ and variance $\frac{\sigma^2}{n}$. 

The normal table tells us that $\Phi(1.96) = 0.975$. In other words $\prob(S < 1.96) = 0.975$, where $S$ is a standard normal variable. This can also be written as $\prob(S > 1.96) = 2.5\%$. By symmetry $\prob(S < -1.96) = 2.5\%$. Thus, $\prob(-1.96 \leq S \leq 1.96) = 95\%$. We use this fact as follows.

We know that 

$$
\frac{\hat\Theta_n - \theta}{\sigma/\sqrt n}
$$

is a standard normal variable. Thus the probability that it lies in $[-1.96, 1.96]$ is $95\%$.

$$
\prob\bigg(\frac{|\hat\Theta_n - \theta|}{\sigma/\sqrt n}\leq 1.96\bigg) = 0.95
$$

We can rewrite this as 

$$
\prob\bigg(\hat\Theta_n -1.96 \frac{\sigma}{\sqrt n} \leq \theta \leq \hat\Theta_n + 1.96 \frac{\sigma}{\sqrt n}\bigg) = 0.95
$$

which implies that 

$$
\bigg[\hat\Theta_n -1.96 \frac{\sigma}{\sqrt n}, \hat\Theta_n + 1.96 \frac{\sigma}{\sqrt n}\bigg]
$$

is a $95\%$ confidence interval.

### Maximum Likelihood Estimation

We have seen that if the unknown parameter can be expressed in the form of expected value of $X$ (or $g(X)$)

$$
\theta = \expect[g(X)]
$$

then $\hat{\Theta}$ can be taken to be the sample mean

$$
\hat{\Theta} = \frac{1}{n}\sum_i g(X_i)
$$

But what if there is no apparent way of treating $\theta$ as an expectation of $X$? In that case, we will use the approach of Maximum Likelihood Estimation. We will pick $\theta$ that makes the data most likely

$$
\hat{\theta}_{ML} = g_{ML}(x) = \operatorname*{arg\,max}_{\theta} p_X(x;\theta)
$$

Operationally, Maximum Likelihood Estimation is quite similar to Bayesian Estimation. There we try to pick a value of $\Theta$ for which the posterior probability $p_{\Theta \mid X}$ is the maximum. If you take the prior to be equal for all $\Theta$, then the MAP Bayesian Estimator would be the value which has maximum likelihood probability $p_{X \mid \Theta}$ (using Bayes' Rule). Maximizing $p_{X \mid \Theta}$ is similar to maximizing $p_X(x ; \theta)$ in Classical Inference.

Despite the similarity in mechanics, the two methods are philosophically very different. In Bayesian setting, you are asking what is the most likely value of $\Theta$, where as in the Classical setting, you are asking which value of $\theta$ makes the observation most likely (least surprising).

Finally we study an example of Maximum Likelihood Estimation, where we try to estimate the bias of a coin, given we get $K$ heads on tossing the coin $n$ times. The first step is to write the likelihood function of data 

$$
p_K(k; \theta) = \Comb{n}{k} \theta^k (1-\theta)^{n-k}
$$

Instead of maximizing this expression, it is easier to maximize the logarithm of this expression (log-likelihood)

$$
\textrm{log}\Comb{n}{k} + k\textrm{ log}(\theta) + (n-k)\textrm{ log}(1-\theta)
$$

To maximize this expression, we take the derivation with respect to $\theta$, which leads to the following formula:

$$
\hat\theta_{ML} = \frac{k}{n}
$$

Or, in terms of random variables

$$
\hat\Theta_{ML} = \frac{K}{n}
$$

[Lec 20.10](https://www.youtube.com/watch?v=00krscK7iBA&list=PLUl4u3cNGP60hI9ATjSFgLZpbNJ7myAg6&index=207) goes over this example. It also discusses how to derive Maximum Likelihood estimate for the mean of a Gaussian Distribution. We see that for this mean inference problem, $\hat\Theta_{ML}$ is the same as the estimate that we obtained earlier using the estimator $g(X) = \sum{X_i}/n$



## Hypothesis Testing

### Binary Hypothesis Testing

Binary Hypothesis Testing is an inference problem where $\theta$ can take just two values. For historical reasons, we forgo the $\theta$ notation and denote the two hypotheses as $H_0$ and $H_1$. $H_0$ is often called the null hypothesis and $H_1$ the alternative hypothesis. $H_0$ plays the role of a default model, to be proved or disproved on the basis of available data.

The available observation is a vector $X = (X_1,\dots,X_n)$ of random variables whose distribution depends on the hypothesis. $\prob(X \in A ; H_j)$ denotes the probability that the sample $X$ belongs to a set $A$, when hypothesis $H_j$ is true. Again $\prob(X \in A ; H_j)$ does not denote conditional probabilities. We want to find a decision rule $g$, that maps the realized values $x$ of the observation to one of the two hypotheses.

![image-20200705101913823](/assets/images/probability/classical_inference.assets/image-20200705101913823.png)Any decision rule can be represented by the partition of the set of all possible values of the observation vector $X$ into two subsets, a set $R$ called the Rejection Region, and its complement $R_c$, the Acceptance Region. Hypothesis $H_0$ is rejected if the observation lies in the rejection region and accepted otherwise. Thus choosing a decision rule is the same as choosing a rejection region.

For a particular choice of the rejection region $R$, there are two possible types of errors:

1.  Reject $H_0$ even though $H_0$ is true. This is called **Type I** error, or a **false rejection**, and happens with probability $\alpha(R) = P(X \in R; H_0)$.
2. Accept $H_0$ even though $H_0$ is false. This is called **Type II** error, or a **false acceptance**, and happens with probability $\beta(R) = P(X \notin R; H_1)$.  

Let us define the Likelihood Ratio $L(x)$ as follows:

$$
L(x) = \frac{\prob_X(x;H_1)}{\prob_X(x;H_0)}
$$

We see that the Likelihood Ratio will be larger, if the probability of making the observation $x$ given the alternative hypothesis is true, is more than the probability of making the observation given the null hypothesis is true. Thus, more the likelihood ratio, the more probability of rejecting $H_0$.

We define the rejection regions as follows:

$$
R = \{ x \mid L(x) > \xi \}
$$

$\xi$ is called the critical value. The special case where $\xi = 1$ corresponds to the maximum likelihood rule.

Note that choosing $\xi$ trades off the probabilities of the two types of errors. As $\xi$ increases, the rejection region becomes smaller. As a result, the false rejection probability $\alpha(R)$ decreases while false acceptance probability $\beta(R)$ increases. Because of this trade-off there is no single best way to choose $\xi$. The most popular approach is as follows:

![Likelihood Ratio Test](/assets/images/probability/classical_inference.assets/image-20200705031231075.png)

When $L(X)$ is a continuous random variable, the probability $\prob(L(X) > \xi; H_0)$ moves continuously from 1 to 0 as $\xi$ increases. Thus, we can find a value of $\xi$ for which the requirement $\prob(L(X) > \xi; H_0) = \alpha$ is satisfied. If, however, $L(X)$ is a discrete random variable, it may be impossible to satisfy the equality $\prob(L(X) > \xi; H_0) = \alpha$ exactly, no matter how $\xi$ is chosen. In such cases, there are several possibilities:

1. Strive for approximate equality.
2. Choose the smallest value of $\xi$ that satisfies $P(L(X) > \xi; Ho) \leq \alpha$.

### Significance Testing

Hypothesis testing problems encountered in realistic settings do not always involve two well-specified alternatives, so the methodology in the preceding section cannot be applied. The purpose of this section is to introduce an approach to this more general class of problems.

Consider problems such as the following:
1. A coin is tossed repeatedly and independently. Is the coin fair?
2. A die is tossed repeatedly and independently. Is the die fair?
3. We observe a sequence of i.i.d. normal random variables $X_1, X_2, \dots, X_n$. Are they standard normal?

In all of the above cases we are dealing with a phenomenon that involves uncertainty, presumably governed by a probabilistic model. We have a default hypothesis, usually called the null hypothesis, denoted by $H_0$, and we wish to determine on the basis of the observations $X = (X_1 ,\dots, X_n)$ whether the null hypothesis should be rejected or not.

We will mostly restrict the scope of our discussion to situations with the following characteristics:

1. **Parametric models**: We assume that the observations $X_1,\dots,X_n$ have a distribution governed by a joint PMF (discrete case) or a joint PDF (continuous case), which is completely determined by an unknown parameter $\theta$ (scalar or vector) belonging to a given set $M$ of possible parameters.
2. <b>Simple null hypothesis</b>: The null hypothesis asserts that the true value of $\theta$ is equal to a given element $\theta_0$ of $M$.
3. <b>Alternative hypothesis</b>: The alternative hypothesis, denoted by $H_1$, is just the statement that $H_0$ is not true, i.e., $\theta \neq \theta_0$. Thus, $H_1$ is not a particular value for $\theta$, but a set of values.

We introduce the general approach through a concrete example.

**Is My Coin Fair?** A coin is tossed independently $n = 1000$ times. Let $\theta$ be the unknown probability of heads at each toss. The set of all possible parameters is $M= [0,1]$. The null hypothesis is that the "coin is fair" or $\theta = 1/2$. Alternative hypothesis is $\theta \neq 1/2$.

The observed data is a sequence $ X_1, \dots, X_n$where $X_i$ is $1$ if i-th toss is heads and $0$ if it is tails. We define $S = X_1 + \dots + X_n$, and decision rule is as follows

$$
\mathrm{reject \; H_0 \; if \;\bigg|S - \frac{n}{2} \bigg| > \xi}
$$

where $\xi$ is a suitable critical value,  to be determined. We finally choose the critical value $\xi$ so that the probability of false rejection is equal to a given value $\alpha$:

$$
\prob(\mathrm{reject\;H_0; H_0 }) = \alpha
$$

$\alpha$ is called the significance level, is a small number. 

Under the null hypothesis, the random variable $S$ is binomial with parameters $n = 1000$ and $p = 1/2$. If we set $\alpha = 0.05$, then using the normal approximation to the binomial and the normal tables, we find that approximately $\xi = 31$.

We summarize and generalize the essence of the example as below

![Significance Testing](/assets/images/probability/classical_inference.assets/image-20200705032416007.png)

Given a value of $\alpha$, if the hypothesis $H_0$ ends up being rejected, one says that $H_0$ is rejected at the $\alpha$ significance level. It does not mean that the probability of $H_0$ being true is less than $\alpha$. Instead, it means that when this methodology is used, we will have false rejections a fraction $\alpha$ times. Rejecting a hypothesis at the 1% significance level means that the observed data is highly unusual under the model associated with $H_0$; such that the data would arise only 1% of the time, and thus provides strong evidence that $H_0$ is false.  

Quite often, statisticians skip steps (c) and (d) in the above described methodology. Instead, once they calculate the realized value $s$ of $S$, they determine and report an associated **p-value** defined by

$$
p\textrm{-value} = \min \alpha, \textrm{ s.t. } H_0 \textrm{would be rejected at the } \alpha \textrm{ significance level }
$$

Equivalently, the $p$-value is the false rejection acceptance rate for which $s$ would just get rejected. Thus, for example, the null-hypothesis will be rejected at the 5% significance level if and only if the $p$-value is smaller than 0.05. 

"$p$-value of a statistic $S=s$ is $p$" implies that the probability of $S$ assuming a value of $s$ or anything less likely than $s$ is $p$ under the null hypothesis. You can either report $s$ with its $p$-value, or you can have a fixed significance level. If $p$-value for the observation is greater than significance level then we do not reject $H_0$ and if $p$-value is less than the significance level then we reject $H_0$.

[Videos by Khan Academy](https://www.khanacademy.org/math/ap-statistics/tests-significance-ap/idea-significance-tests/v/p-values-and-significance-tests) are also great for understanding significance-testing and $p$-values. Observe that the null and alternative hypothesis in these videos doesn't exactly fit the criterion for alternative hypothesis specified above.

