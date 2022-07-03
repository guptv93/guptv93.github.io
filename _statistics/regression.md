---
layout: default
title: Regression
slug: regression
item_num: 7
excerpt: Regression is a method for studying the relationship between a response variable and a covariate/feature. Here we study Linear Regression, specifically how to find good least sum of squares estimator, how to find the distribution of these estimators and how to perform inference for true parameters.
---

$$
\newcommand{\expect}{\mathrm{E}}
\newcommand{\prob}{\mathrm{P}}
\newcommand{\v}{\mathrm{var}}
$$



# Regression



## Introduction

Regression is a method for studying the relationship between a **response variable** $Y$ and a **covariate** $X$. The covariate is also called a predictor variable or a feature. The **regression function** (depicting the relationship between $X$ and $Y$) is given as follows:

$$
r(x) = \expect(Y \vert X = x) = \int {y f(y\vert x) dy}
$$

Our goal is to estimate the regression function $r(x)$ from data of the form

$$
(Y_1, X_1), \dots, (Y_n, X_n) \sim F_{X,Y}
$$

In **Simple Linear Regression**, we take a parametric approach and assume that $r$ is linear. If $X_i$ is one-dimensional, we have:

$$
r(x) = \expect(Y | X=x) = \alpha + \beta x
$$

Another way to write this is 

$$
Y = \alpha + \beta X + \epsilon
$$

where $\expect(\epsilon \vert X) = 0$. We will make another simplifying assumption that $\v(\epsilon \vert X = x) = \sigma^2$ and is independent of $x$. The assumptions of linearity and equal variance help in making inferences (explained later).

The unknown parameters in the model are the intercept $\alpha$, the slope $\beta$ and the variance $\sigma^2$. We make observations $(X_i, Y_i)$ and try to estimate these unknown parameters. Let $A$ and $B$ denote estimates of $\alpha$ and $\beta$. The *fitted line* is 

$$
\hat r(x) = A + Bx
$$

The **predicted values** or **fitted values** are $\hat{Y}_ i = \hat{r}(X_i)$ and the **residuals** are defined to be 

$$
\hat\epsilon_i = Y_i - \hat Y_i = Y_i - \bigg (A + Bx\bigg)
$$


## Least Squares Estimators

The **sum of squares of the residuals**, which measures how well the line fits the data, is defined by  

$$
SS_R = \sum_i\hat\epsilon_i^2 = \sum_i \bigg [ Y_i - \big (A + Bx\big) \bigg ]^2
$$

The **least squares estimates** are the values of $A$ and $B$ that minimize residual sums of squares. If we let $S$ denote the *sample* covariance of two random variables, specifically

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
B &= \frac{\sum_i(X_i - \bar X_n)(Y_i - \bar{Y}_n)}{\sum_i(X_i - \bar X_n)^2} = 
\frac{S_{XY}}{S_{XX}} \\
A &= \bar Y_n - B\bar X_n\\
\end{align}
$$

This formula can be derived by expanding the formula for $SS_R$ and equating its gradient to zero (minima condition). 

Substituting the values of $A$ and $B$, we get

$$
\begin{align}
\hat Y &= A + BX \\
&= \bar Y_n - B \bar X_n + B X \\
&= \bar Y_n + B(X - \bar X_n) \\
&= \bar Y_n + \frac{S_{XY}}{S_{XX}}(X - \bar X_n) \\
\end{align}
$$

The formula above has an intuitive interpretation. The estimator starts with the baseline estimate $\bar Y_n$, which it then adjusts by taking into account the value of $X - \bar X_n$. Suppose $S_{XY}$ is positive. This means that the estimator should increase in proportion to $X - \bar X_n$. The least squares estimate equation shows that the proportionality constant is $B = \frac{S_{XY}}{S_{XX}}$. If $S_{XY} = 0$, then $X$ and $Y$ are not correlated, so a given value of $X$ should not affect the value of the dependent variable $Y$.

Note that $B = \frac{S_{XY}}{S_{XX}} = r\frac{\sigma_Y}{\sigma_X}$, where $r$ is the *sample* correlation coefficient and $\sigma$ denotes the *sample* standard deviation of the respective variable. See the following videos by Khan Academy for an example of how to calculate the correlation coefficient and the equation of regression line: [Correlation Coefficient](https://www.youtube.com/watch?v=u4ugaNo6v1Q), [Regression Line](https://www.youtube.com/watch?v=FGesqq22TCM).

Using the least squares estimator value of $A$, we can verify that the intercept term ensures that the average residual is zero.

$$
\begin{align}
\sum_i\hat\epsilon_i &= \sum_i(Y_i - \hat Y_i) \\
&= \sum_i \bigg[ Y_i - \bigg (A + B X_i\bigg)\bigg] \\
&=n\bar Y_n - nA - n\bar X_nB \\
&= 0 \\
\end{align}
$$

If the average residual is positive, then we reduce the value of the intercept till the average is zero. Similarly, we decrease the value of the intercept in case the average residual is negative. In other words, the constant term prevents the model from making predictions that are systematically too high or too low.

Also note that, when the $Y_i$(s) are normal random variables, the least square estimators are also the maximum likelihood estimators. To verify this remark, we just need to simplify the joint distribution of $Y_1, \dots, Y_n$ (assume all probabilities below are given $X_1, \dots, X_n$):

$$
\begin{align}
f_{Y_1, \dots, Y_n} (y_1, \dots, y_n) &= \prod_i f_{Y_i}(y_i) \\
&= \prod_i \frac{1}{\sigma\sqrt{2\pi}} e^{(y_i - \alpha -\beta x_i)^2/2\sigma^2} \\
&= \frac{1}{(2\pi)^{n/2}\sigma^n} e^{\sum_i(y_i - \alpha -\beta x_i)^2/2\sigma^2}\\
\end{align}
$$

 Consequently, the maximum likelihood estimators of $\alpha$ and $\beta$ are precisely the values of $\alpha$ and $\beta$ that minimize $\sum_i (y_i − α − \beta x_i)^2$. That is, they are the least squares estimators. Remember that, the assumption of $Y \sim \mathcal{N}(\alpha + \beta X, \sigma^2)$ is needed for Maximum Likelihood Estimation, but not for Least Squares Estimation



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
\expect(A) &= \alpha \tag{1}\\
\expect(B) &= \beta \tag{2}\\
\v(B) &= \frac{\sigma^2}{S_{XX}} \tag{3} \\
\expect\bigg[\frac{SS_R}{n-2}\bigg] &= \sigma^2 \tag{4} \\
A, B &\sim \mathcal{N} \tag{5} \\
\end{align*}
$$

We will accept the above results without proof. Refer to Section 9.3 of [Introduction to Probability and Statistics for Engineers](https://www.amazon.com/dp/0128243465), for full derivations of the above identities.



##  Inference in Linear Regression

Now that we can calculate the values of our estimators $A$ and $B$, and also derive their distributions; it is time to make inferences about the true regression parameters $\alpha$ and $\beta$.

An important hypothesis to consider regarding the simple linear regression model

$$
Y = \alpha + \beta X + \epsilon
$$

is the hypothesis that $\beta = 0$. Its importance derives from the fact that it is equivalent to stating that the mean response does not depend on the input, or, equivalently, that there is no regression on the input variable. To test

$$
H_0 : \beta = 0 \; \; \mathrm{versus} \; \; H_1 : \beta \neq 0 
$$

From the identities in the previous section, we can conclude that:

$$
\frac{B - \beta}{\hat{\v}(B)} = \frac{(B - \beta)\sqrt{(n - 2)S_{XX}}}{\sqrt{SS_R}} \sim t_{n-2}
$$

Remember that $B$ is a random variable and $\beta$ is an unknown constant. If $\beta = 0$ then 

$$
B\sqrt{\frac{(n - 2)S_{XX}}{SS_R}} \sim t_{n-2}
$$

which gives rise to the following test for $H_0$:

A significance level $v$ test of $H_0$ is to

$$
\text{reject $H_0$ if } \vert B \vert \sqrt{\frac{(n - 2)S_{XX}}{SS_R}} > t_{v/2, n-2}\\
\text{accept $H_0$ otherwise }
$$

We can also perform classical interval estimation for $\beta$ in a similar fashion (using the distribution of $B$). For more details refer to Khan Academy videos on [Inference about Slope](https://www.khanacademy.org/math/statistics-probability/advanced-regression-inference-transforming#inference-on-slope). 