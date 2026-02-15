---
layout: default
title: Regression
slug: regression
item_num: 7
excerpt: Regression is a method for studying the relationship between a response variable and a covariate/feature. Here we study Linear Regression only from a Classical Inference perspective. We learn how to compute the least sum of residual squares estimator, how to understand these estimators from a MLE perspective, and how to perform inference for true parameters.
---

$$
\newcommand{\expect}{\mathrm{E}}
\newcommand{\prob}{\mathrm{P}}
\newcommand{\v}{\mathrm{var}}
\newcommand{\Comb}[2]{ {}^{#1}C_{#2} }
\newcommand{\mff}{\mathfrak{F}}
$$



# Regression

Regression is the process of building a model of the relation between two or more variables of interest on the basis of available data. 

Let $X$  be the independent variable and $Y$ be the dependent variable. There is some deterministic relationship between $Y$ and $X$ of the very general form:   


$$
r(x) = \expect(Y \vert X = x)
$$


We *assume* that the function $r$ belongs to a fixed set of functions, $\mff$, known as the regression model. The process of finding the best fit ($f \in \mff$) for $r$, based on the available data is called **regression**. 

In **Simple Linear Regression**, we take a parametric approach and assume that $r$ is linear. If $X_i$ is one-dimensional, we have:

$$
r(x) = \expect(Y | X=x) = \alpha + \beta x
$$

Another way to write this is 

$$
Y = \alpha + \beta X + \epsilon
$$

where $\expect(\epsilon \vert X) = 0$. To verify this, define $\epsilon = Y - r(X)$ and take conditional expectation on both sides. Also $\expect(\epsilon) = \expect\bigg(\expect(\epsilon \vert X)\bigg) = 0$.



## Least Sum of Squares Estimator

We make observations $(X_i, Y_i)$ and try to fit a line to these observations. The *fitted line* is 

$$
\hat Y = A + Bx
$$

The **predicted values** or **fitted values** are $\hat{Y}_ i$ and the **residuals** are defined to be 

$$
\hat\epsilon_i = Y_i - \hat Y_i = Y_i - \bigg (A + Bx\bigg)
$$

The **sum of squares of the residuals**, which measures how well the line fits the data, is defined by  

$$
SS_R = \sum_i\hat\epsilon_i^2 = \sum_i \bigg [ Y_i - \big (A + Bx\big) \bigg ]^2
$$

The **least squares estimates** are the values of $A$ and $B$ that minimize residual sums of squares. To determine these estimators, we differentiate $SS_R$ first with respect to $A$ and then to $B$.

If we let $\bar{Y}$ denote average of all $Y_i$s and $S$ denote the *sample* covariance of two random variables,  specifically
$$
\begin{align}
S_{XY} &= \sum_{i = 1}^n(X_i - \bar{X})(Y_i - \bar{Y}) \\
S_{XX} &= \sum_{i = 1}^n(X_i - \bar{X})^2 \\
S_{YY} &= \sum_{i = 1}^n(Y_i - \bar{Y})^2 \\
\end{align}
$$

then the least squares estimates are given by 

$$
\begin{align}
B &= \frac{\sum_i(X_i - \bar X)(Y_i - \bar{Y})}{\sum_i(X_i - \bar X)^2} = 
\frac{S_{XY}}{S_{XX}} \\
A &= \bar Y - B\bar X\\
\end{align}
$$

Substituting the values of $A$ and $B$, we get

$$
\begin{align}
\hat Y &= A + BX \\
&= \bar Y - B \bar X + B X \\
&= \bar Y + B(X - \bar X) \\
&= \bar Y + \frac{S_{XY}}{S_{XX}}(X - \bar X) \\
\end{align}
$$

The formula above has an intuitive interpretation. The estimator starts with the baseline estimate $\bar Y_n$, which it then adjusts by taking into account the value of $X - \bar X$. Suppose $S_{XY}$ is positive. This means that the estimator should increase in proportion to $X - \bar X_n$. The least squares estimate equation shows that the proportionality constant is $B = \frac{S_{XY}}{S_{XX}}$. If $S_{XY} = 0$, then $X$ and $Y$ are not correlated, so a given value of $X$ should not affect the value of the dependent variable $Y$.

Note that $B = \frac{S_{XY}}{S_{XX}} = r\frac{\sigma_Y}{\sigma_X}$, where $r$ is the *sample* correlation coefficient and $\sigma$ denotes the *sample* standard deviation of the respective variable. See the following videos by Khan Academy for an example of how to calculate the correlation coefficient and the equation of regression line: [Correlation Coefficient](https://www.youtube.com/watch?v=u4ugaNo6v1Q), [Regression Line](https://www.youtube.com/watch?v=FGesqq22TCM).

Using the least squares estimator value of $A$, we can verify that the intercept term ensures that the average residual is zero.

$$
\begin{align}
\sum_i\hat\epsilon_i &= \sum_i(Y_i - \hat Y_i) \\
&= \sum_i \bigg[ Y_i - \bigg (A + B X_i\bigg)\bigg] \\
&=n\bar Y - nA - n\bar XB \\
&= 0 \\
\end{align}
$$

If the average residual is positive, then we reduce the value of the intercept till the average is zero. Similarly, we decrease the value of the intercept in case the average residual is negative. In other words, the constant term prevents the model from making predictions that are systematically too high or too low.



## Classical Perspective to Linear Regression

Using the Least Square Estimators above, we can fit a line over any given data (linear or not). However, the fitted line will not mean much if there is no probabilistic justification for it. In this section, we develop a probabilistic justification for the least squares estimators, using Maximum Likelihood Estimation in Classical Statistics.

We assume that the $x_i$ are given numbers (not random variables). We assume that $y_i$ is the realization of a random variable $Y_i$, generated according to the above mentioned linear regression model


$$
\begin{align*}
Y_i = \alpha + \beta x_i + \epsilon_i && i = 1, 2, 3, ..., n
\end{align*}
$$
where the $\epsilon_i$ are i.i.d. normal random variables with mean zero and variance. It follows that the $Y_i$ are independent normal variables, where $Y_i$ has mean $\alpha + \beta x_i$ and variance $\sigma^2$. In this case, the probability of observations $y_1, y_2, \dots, y_n$ is given as follows:
$$
\begin{align}
f_{Y_1, \dots, Y_n} (y_1, \dots, y_n; \alpha, \beta) &= \prod_i f_{Y_i}(y_i; \alpha, \beta) \\
&= \prod_i \frac{1}{\sigma\sqrt{2\pi}} e^{-(y_i - \alpha -\beta x_i)^2/2\sigma^2} \\
&= \frac{1}{(2\pi)^{n/2}\sigma^n} e^{-\sum_i(y_i - \alpha -\beta x_i)^2/2\sigma^2}\\
\end{align}
$$

Here $\alpha, \beta$ are unknown parameters. Let us say $A$ and $B$ are our estimators of $\alpha$ and $\beta$. Then we pick the values of $A$ and $B$ so that the likelihood of our observations is the maximum (MLE). 
$$
\begin{align*}
A, B &= \max_{\alpha, \beta} f_{Y}(Y; \alpha, \beta) \\
&= \max_{\alpha, \beta} \frac{1}{(2\pi)^{n/2}\sigma^n} e^{-\sum_i(Y_i - \alpha -\beta x_i)^2/2\sigma^2} \\
&= \max_{\alpha, \beta}{-\sum_i(Y_i - \alpha -\beta x_i)^2/2\sigma^2} &\text{maximize exponent} \\
&= \min_{\alpha, \beta}\sum_i(Y_i - \alpha -\beta x_i)^2
\end{align*}
$$
Thus, Maximum Likelihood Estimation leads to the same estimates that we get to through Least Squares Estimation. Remember that the assumption of $Y_i \sim \mathcal{N}(\alpha + \beta x_i, \sigma^2)$, is needed for Maximum Likelihood Estimation, but not for Least Squares Estimation. We will see in the next section that making these assumptions, helps us to go beyond point estimates and to derive entire distributions for $A$ and $B$.



## Distribution of the Estimators

In order to go over and above least squares estimation, and make actual inferences about the true parameters $\alpha$ and $\beta$, we need to derive the distribution of our estimators $A$ and $B$. But for this, it is necessary to make certain assumptions

1. **L**inearity: $\expect(Y \vert X)$ has a linear relationship with $X$, implying $\expect(\epsilon \vert X) = 0$
2. **I**ndependence: Individual observations $(X, Y)$ are independent of each other
3. **N**ormality: For any given value of $X$, the residual $\epsilon$ is normally distributed
4. **E**quality of Variance: $\v(\epsilon \vert X)$ is independent of $X$
5. **R**andomness: The observations are made randomly

Overall, the above assumptions can be summarized as: $(X_i, Y_i)$ are i.i.d samples with
$$
Y_i \sim \mathcal{N}(\alpha + \beta X_i, \sigma^2)
$$
With these assumptions, we can prove the following identities:

$$
\begin{align*}
A &\sim \mathcal{N}\bigg(\alpha, \frac{\sigma^2\sum_ix_i^2}{nS_{XX}}\bigg) \tag{1}\\
B &\sim \mathcal{N}\bigg(\beta, \frac{\sigma^2}{S_{XX}}\bigg) \tag{2}\\
\expect&\bigg[\frac{SS_R}{n-2}\bigg] = \sigma^2 \tag{3} \\
\end{align*}
$$

Refer to Section 9.3 of [Introduction to Probability and Statistics for Engineers](https://www.amazon.com/dp/0128243465), for full derivations of the above identities.

Now that we know that the expected value of $A$ is $\alpha$ and $B$ is $\beta$, and that we have a way to estimate $\sigma^2$; we can calculate confidence intervals and perform statistical significance testing for $\alpha$ and $\beta$.



## The Coefficient of Determination $R^2$

We use linear regression to predict $Y$ given some value of $X$. But suppose that we had to predict a $Y$ value without a corresponding $X$ value. Without using regression on the $X$ variable, our most reasonable estimate would be to simply predict the average of the $Y$ values.

One way to measure the fit of the line is to calculate the sum of the squared residuals—this gives us an overall sense of how much prediction error a given model has. The sum of squared residuals for the mean prediction model is equal to the sample variance of $Y$, denoted as $S_{YY}$.

Would using least-squares regression reduce the amount of prediction error? If so, by how much? Let us denote the sum of the squared residuals for the least-squares regression line by $SS_R$. Thus,

$$
S_{YY} - SS_R
$$

represents the amount of variation in the response variables that is *explained* by the different input values; and so the Coefficient of Determination (denoted by $R^2$), defined as

$$
\begin{align}
R^2 &= \frac{S_{YY} - SS_R}{S_{YY}} \\
&= 1 - \frac{SS_R}{S_{YY}}
\end{align}
$$

represents the proportion of the variation in the response variables that is explained by the least squares regression.

The Coefficient of Determination $R^2$ will have a value between $0$ and $1$. A value of $R^2$ near $1$ indicates that most of the variation of the response data is explained by the regression line, whereas a value of $R^2$ near $0$ indicates that little of the variation is explained by the fitted line.

It seems pretty remarkable that simply squaring $r$ gives us the Coefficient of Determination $R^2$. But intuitively, it makes sense that as the correlation between $X$ and $Y$ increases, the amount of variability in $Y$ that can be explained by variability in $X$ also increases. We will not go into the details of the exact derivation. 



## Optional Readings

1. Section 9.2 of [Introduction to Probability, Bertesekas, Tsitsiklis] briefly goes over how to perform Regression under the Bayesian Framework and how different priors lead to different MAP estimates.

2. Section 9.6 of [Introduction to Probability and Statistics for Engineers](https://www.amazon.com/dp/0128243465) tells us how to analyze the residuals to ensure that the conditions for linear regression are being met.