---
layout: default
title: Further Topics on Random Variables
slug: further-topics
item_num: 5
excerpt: We have already seen how to derive the distribution of a function of a random variable $Y = g(X)$, given the distribution of $X$ itself. Here we learn how to derive distribution of the convolution of two different variables, and calculate their correlation and covariance. Covariance and Correlation play an important role in predicting value of one random variable, given another random variable (machine learning).
---


$$
\newcommand{\expect}{\mathrm{E}}
\newcommand{\prob}{\mathrm{P}}
\newcommand{\v}{\mathrm{var}}
\newcommand{\cov}{\mathrm{cov}}
\newcommand{\Comb}[2]{ {}^{#1}C_{#2} }
\newcommand{\mat}[1]{\begin{bmatrix} #1 \end{bmatrix}}
\newcommand{\bt}[1]{\mathbf{#1}}
\newcommand{\notimplies}{\;\not\!\!\!\implies}
$$

# Further Topics on Random Variables



## Derived Distributions 

*Lecture 11*

Here we learn how to derive the distribution of a function of a random variable $Y = g(X)$, given the distribution of $X$ itself. We learn how to do that for discrete and continuous variables separately and then devise a common approach for both kinds using cummulative densities. 

Note that the expected value of a function of random variable can be found out directly by using the formula:

$$
\expect[g(X)] = \int_{-\infty}^{+\infty}g(x)p_X(x)dx
$$

What we study here is needed only in case we need the full distribution. Finally we learn how to find distribution for $Z = g(X,Y)$ given the joint distribution for $X$ and $Y$.   

**Discrete Random Variable**

Suppose $Y = aX + b$. We need to find the PMF for $Y$.

$$
\begin{align}
p_Y(y) &= \prob(Y=y) \\
&= \prob(aX+b = y) \\
&= \prob(X = \frac{y-b}{a}) \\
&= p_X(\frac{y-b}{a})
\end{align}
$$

Thus, 

$$
Y = aX+b \implies p_Y(y) = p_X(\frac{y-b}{a})
$$

**Continuous Random Variable**

Here $F$ denotes the CDF. Let $Y = aX + b$ be the derived variable.

$$
\begin{align}
F_Y(y) &= \prob(Y \leq y) \\
&= \prob(aX+b \leq y) \\
&= \prob(X \leq \frac{y-b}{a}) & \text{when a > 0, inverse otherwise}\\
&= F_X(\frac{y-b}{a})
\end{align}
$$

Differentiating w.r.t. $y$ gives us, 

$$f_Y(y) = \frac{1}{\mid a \mid}f_X(\frac{y-b}{a})$$  

This makes intuitive sense. The PDF graph of $Y=aX+b$ is the same as that of $X$, but only horizontally stretched by $a$ and translated horizontally by $b$. If we stretch a graph by $a$, the area under the graph also gets scaled by $a$. Therefore, in order to keep the area under the graph equal to $1$, we need to divide by $\mid a \mid$.  

*The above result also proves that, if $X \sim N(\mu, \sigma^2)$, then $aX +b \sim N(a\mu + b, a^2\sigma^2)$. It is very easy to prove using the formula above. In case you need help, refer to the [slides](https://ocw.mit.edu/resources/res-6-012-introduction-to-probability-spring-2018/part-i-the-fundamentals/MITRES_6_012S18_L11AS.pdf).*

We can use the above described technique (using CDF) to derive the distribution of any general function $g(X)$ (not necessarily linear). The two step procedure is as follows:

* Find the CDF of $Y$:

$$
F_Y(y) = \prob(Y < y) = \prob(g(X) \leq y)
$$

* Differentiate:

$$
f_Y(y) = \frac{dF_Y}{dy}(y)
$$

Now we will derive a general formula for the PDF of $Y = g(X)$, when $g$ is monotonic. Assume $g$ is strictly increasing and differentiable. Let $h$ be the inverse function of $g$. Then,  

$$
\begin{align}
F_Y(y) &= \prob(Y \leq y)\\
&= \prob(X \leq h(y)) & \textrm{ because of monotonicity} \\
&= F_X(h(y)) \\
\therefore f_Y(y) &= f_X(h(y)) |\frac{dh}{dy}(y)|
\end{align}
$$

<img src="/assets/images/probability/further_topics.assets/image-20200629003401262.png" alt="image-20200629003401262"  />

Till now we have considered the case where $Y$ is a function of $X$ (linear / monotonic / non-monotonic). What if the random variable of interest $Z$ is a function of two independent random variables $X$ and $Y$? How do we calculate the PDF of $Z = g(X,Y)$ in that case? The method remains the same. We use the joint probability distribution of $X$ and $Y$ to somehow find the CDF of $Z$. Then we differentiate the CDF to find the PDF of $Z$. See [Lec 11.9](https://www.youtube.com/watch?v=X-krLprDrOI&list=PLUl4u3cNGP60hI9ATjSFgLZpbNJ7myAg6&index=119) for an example of the same.



## Convolution, Covariance and Correlation 

*Lecture 12*

### Overview

Here we see how to calculate the PMF/PDF of $X + Y$ when $X$ and $Y$ are independent variables (continuous and discrete) and specifically when $X$ and $Y$ are independent normals ($X+Y$ is also a normal in this case). These are all special cases of the $Z=g(X,Y)$ scenario studied in Derived Distributions.  Finally we study covariance and correlation. Covariance and Correlation play an important role in predicting value of one random variable, given another random variable (machine learning).

### Sum of Independent Random Variables

**The Discrete Case**

The PMF of $Z = X + Y$, when $X$ and $Y$ are independent and discrete, is given by:

$$
\prob_Z(z) = \sum_x\prob(X=x,Y=z-x) = \sum_x\prob_X(x)\prob_Y(z-x)
$$

The above operation, of deriving the distribution of the sum of two random variables, is known as *convolution* of those random variables.

How do you calculate the value of convolution for a given value of $Z$ (denoted by $z$)? You flip (horizontally) the PMF of $Y$. Then shift it to the right by $z$. Finally, element wise cross mutliply the derived PMF with the PMF of $X$ and add each term together. This will give you the value of $\prob_Z$ for one specific $z$.

**The Continuous Case**

The convolution of continuous independent random variables $X$ and $Y$ is given by:

$$
f_Z(z) = \int_{-\infty}^{+\infty}f_X(x)f_Y(z-x)\,dx
$$

The mechanics of calculating the convolution are the same for the continuous case (flip, shift, etc.)

Let us now come to the specific case where $X$ and $Y$ are independent normal variables. Let $Z = X + Y$.

<img src="/assets/images/probability/further_topics.assets/image-20200629131506466.png" alt="image-20200629131506466" style="zoom: 67%;" />

Thus, $Z$ is also a normal variable with mean $\mu_x + \mu_y$ and variance of $\sigma_x^2 + \sigma_y^2$. The mean and variance can also be derived easily using the Linearity of Expected Values and Linearity of Variances for Independent Variables.



### Covariance

Covariance basically tells us if two variables $X$ and $Y$ vary in the same or different directions from their respective means. Positive Covariance indicates that $X$ and $Y$ go above/below their respective means simultaneously. Negative Covariance indicates that when $X$ goes above its mean, $Y$ goes below, and vice-versa.

$$
\cov(X,Y) = \expect[(X - \expect[X])(Y - \expect[Y])]
$$

If $X$ and $Y$ are zero-mean random variables, then covariance is given by $\expect[XY]$. If both $X$ and $Y$ increase and decrease in tandem, then the values of $X$ vs $Y$ graph will lie in first and third quadrant and the covariance will be positive. If $Y$ decrease when $X$ increase and vice-versa, then the values will lie in second and forth quadrant and the covariance will be negative. If the two random variables are independent, then the covariance becomes $$\expect[XY] = \expect[X]\expect[Y] = 0\cdot 0 = 0$$ 

The covariance of independent variables is always zero, but variables whose covariance is zero are not always independent. In the figure below, it is evident that the covariance is zero (either $X$ or $Y$ is zero $\implies$ $E[XY] = 0$) . However, the two variables are not independent. Knowing that $X=1$ tells us that $Y=0$.

![image-20200629162358155](/assets/images/probability/further_topics.assets/image-20200629162358155.png)

**Properties**

* $\cov(X,X) = \v(X)$
* $\cov(X,Y) = \expect[XY] - \expect[X]\expect[Y]$
* $\cov(aX+b, Y) = a\,\cov(X,Y)$
* Suppose $X_1$ and $X_2$ are dependent random variables. Then $\v(X_1 + X_2) = \v(X_1) + \v(X_2) + 2\cov(X_1, X_2)$  

### Correlation

Correlation is the dimensionless version of covariance. The sign of covariance shows if two variables move away from their respective means in the same direction or different. But it is hard to make sense of the magnitude of covariance. Correlation is defined as an alternative :  

$$
\rho(X,Y) = \expect\Bigg[\frac{X-\expect[X]}{\sigma_X}\times\frac{Y-\expect[Y]}{\sigma_Y}\Bigg] = \frac{\cov(X,Y)}{\sigma_X\sigma_Y}
$$

Notice that the correlation coefficient is the expected value of the product of z-scores of $X$ and $Y$. More on z-scores in a minute.

**Property 1:**

An important property of the correlation coefficient is that it always lies between $-1$ and $1$.  

$$
-1 \leq \rho \leq 1
$$

This allows us to judge whether a given correlation coefficient is small or large (because now we have an absolute scale). Therefore, it provides us a measure of the degree of "association" between $X$ and $Y$. Proof?

If $X$ and $Y$ have zero means and unit variances, then 

$$
\begin{align}
0 \leq \expect[(X-\rho Y)^2] &= E[X^2] - 2 \rho \expect[XY] + \rho^2\expect[Y^2]\\
&= 1 - 2 \rho^2 + \rho^2\\
&= 1 -\rho^2\\
\end{align}
$$

Thus, $\rho^2 \leq1$. All this can also be proved if $X$ and $Y$ don't have unit variance and zero mean, using somewhat more involved calculations.

Also, notice that if $\rho = \pm1$, then $X = \rho Y$, which means $X$ is a linear function of $Y$. 

**Property 2:**

When $X$ and $Y$ are independent, $\cov(X, Y) = 0 \implies \rho(X,Y) = 0$ (converse is not true).

**Property 3:**

We just considered the case where $X$ and $Y$ are independent. Now we look at the other extreme case, where $X$ and $Y$ are as dependent as they can be, i.e. $Y = X$: 

$$
\rho(X,X) = \frac{\v(X)}{\sigma_X^2} = 1
$$

**Property 4:**

$$

\cov(aX + b, Y) = a\,\cov(X, Y) \implies \rho(aX+ b, Y) = \frac{a\,\cov(X, Y)}{|a|\sigma_x\sigma_y} = \textrm{sign}(a)\,\rho(X, Y)
$$

Thus, unlike co-variance, correlation is not affected by linear stretching or contraction. This is an important property that makes correlation meaningful.

**Property 5:**

Combining properties 3 and 4, we can conclude that if $Y = aX + b$, then $\rho(X, Y) = \pm 1$. The correlation coefficient is $\pm 1$, if the variables are linearly related.

$$
\mid\rho\mid = 1 \Leftrightarrow (X-\expect[X]) = c(Y-\expect[Y])
$$

Refer to Lec 12.10 and 12.11 for intuition behind correlation and its practical use. Remember that correlation coefficient can only measure linear dependence between variables. The variables might be dependent (non-linearly) and have correlation coefficient of zero.

<img src="/assets/images/probability/further_topics.assets/correlation_examples.png">

  


### Side Note on Standard Scores

Standard scores (also known as z-scores) give us a way of comparing values across different data sets even when the sets of data have different means and standard deviations. They’re a way of comparing values as if they came from the same set of data or distribution. As an example, you can use standard scores to compare each player’s performance relative to his *own personal* track record—a bit like a personal trainer would.  

Standard scores work by transforming sets of data into a new, theoretical distribution with a mean of 0 and a standard deviation of 1. It’s a generic distribution that can be used for comparisons. Standard scores effectively transform your data so that it fits this model while making sure it keeps the same basic shape.  

Standard scores can take any value, and they indicate position relative to the mean. Positive z-scores mean that your value is above the mean, and negative z-scores mean that your value is below it. If your z-score is 0, then your value is the mean itself. The size of the number shows how far away the value is from the mean.

**Standard Score = Number of Standard Deviations from the Mean**  

Generally, values that are more than three standard deviations away from the mean (z-score > 3) are known as outliers.



## Conditional Expectation and Variance Revisited

*Lecture 13*

### Overview

We will study how conditional expectations and conditional variances can be treated as random variables. $\expect[X \mid Y]$ is a function of $Y$ and thus is itself a random variable. Then we use that knowledge to calculate the expectation and variance of the sum of random number of independent variables. 

### Conditional Expectation as a Random Variable

Let $g(Y)$ be a random variable that takes the value $\expect[X \mid Y=y]$, if $Y$ happens to take the value $y$.

$$
\begin{align}
g(y) &= \expect[X \mid Y=y] \\
g(Y) &= \expect[X \mid Y] \\
\expect[g(Y)] &= \expect[\expect[X \mid Y]] \\
\end{align}
$$

The mean of $E[X \mid Y]$ is given by the Law of Iterated Expectations, which says:

$$
\expect[\expect[X \mid Y]] = \expect[X]
$$

In [Lec 13.4](https://www.youtube.com/watch?v=LVfIS8pBI6Y&list=PLUl4u3cNGP60hI9ATjSFgLZpbNJ7myAg6&index=135) we use Law of Iterated Expectations to solve the stick breaking problem. 

### Conditional Variance as a Random Variable

$\v(X \mid Y)$ is the random variable that takes the value $\v(X \mid Y=y)$, when $Y= y$.  

Law of Total Variance says:

$$
\v(X) = \expect[\v(X \mid Y)] + \v(\expect[X \mid Y])  
$$

In order to get an intuitive understanding of the Law of Total Variance, we consider the example problem of **Section Means and Variances**. We divide the entire set of students (sample space) into multiple sections. The experiment is to pick a student at random. Random variable $X$ denotes the marks of that student and random variable $Y$ denotes the section of that student. 

Here, $\expect[X \mid Y]$ gives the average score of a student in one particular section and $\v(X\mid Y)$ gives the variation in the marks of the students for a particular section. We find the following alternate way of looking at law of total variance:  

<center>
  total variance = average variance <b>within</b> each section + variance <b>between</b> sections
</center>

### Sum of a Random Number of Independent Variables  

Here we learn how to find the mean and variance of the sum of a random number of independent random variables. Let $N$ be a random variable denoting the number of stores visited, and let $X_1, X_2, \dots X_n$ be the money spent at each store. All the $X_i$s are independent identically distributed random variables. They are also independent of $N$. We want to derive details of the random variable $Y$ such that $$Y = \sum_iX_i$$

$$
\begin{align}
\expect[Y \mid N=n] &= \expect[X_1 + \dots + X_N \mid N = n] \\
&= \expect[X_1 + \dots + X_n \mid N = n] \\
&= \expect[X_1 + \dots + X_n] \\
&= n\expect[X]
\end{align}
$$

Now, Total Expectation Theorem says that:

$$
\expect[Y] = \sum_n \bigg(p_N(n)\expect[Y \mid N=n] \bigg) =  \sum_n\bigg( p_N(n)\;n\; \expect[X]\bigg) = \expect[N]\;\expect[X]
$$

This can also be derived using Law of Iterated Expectations:

$$
\expect[Y] = \expect[\expect[Y \mid N]] = \expect[N\expect[X]] = \expect[N]\expect[X]
$$

Total Variance of $Y$ can be derived using Law of Total Variance. The derivation is simple and mundane.

## Appendix

### Covariance Matrix

When working with multiple variables, the covariance matrix provides a succinct way to summarize the covariances of all pairs of variables. In particular, if $\mathbf{X} = (X_1, \dots, X_n)^T$ is a $n \times 1$ multivariate random variable, then the covariance matrix,
which we usually denote as $\Sigma$, is the $n \times n$ matrix whose $(i, j)$th entry is $\cov(X_i, X_j)$. 

$$
\begin{equation}
\underset{n\times n}{\Sigma}=\left(\begin{array}{cccc}
\sigma_{1}^{2} & \sigma_{12} & \cdots & \sigma_{1n}\\
\sigma_{12} & \sigma_{2}^{2} & \cdots & \sigma_{2n}\\
\vdots & \vdots & \ddots & \vdots\\
\sigma_{1n} & \sigma_{2n} & \cdots & \sigma_{n}^{2}
\end{array}\right)
\end{equation}
$$

Refer to [Chapter 3.6 of Bookdown.org](https://bookdown.org/compfinezbook/introcompfinr/Multivariate-Probability-Distributions-Using-Matrix-Algebra.html) for more details. Of particular importance is section 3.6.6, which states that if $\mathbf{Y} = \mathbf{AX} + \mathbf{b}$, then $\Sigma_\mathbf{Y} = \mathbf{A}\Sigma_\mathbf{X}\mathbf{A}^T$. Also take note that in this case, $f_\mathbf{Y}$ has shape similar to $f_\mathbf{X}$ with linear scaling and translation, similar to linear transformation of a univariate normal variable.

Notice that if $X_1, \dots, X_n$ are all independent random variables, then $\Sigma_\mathbf{X}$ is a diagonal matrix.

### Multivariate Normal Distribution

*Sources: [CS229 Handout](/assets/documents/cs229_gaussians.pdf), [Noah Golmant Blog](/assets/documents/noahgolmant_gaussian.pdf)*

We saw that if $X$ and $Y$ are independent normal variables then

$$
f_{X, Y}(x,y) = \frac{1}{2\pi \sigma_x \sigma_y }\textrm{exp}\bigg\{-\frac{(x-\mu_x)^2}{2\sigma_x^2}-\frac{(y-\mu_y)^2}{2\sigma_y^2}\bigg\} 
$$

If we consider $$\bt{X} = \mat{X \\ Y}$$, then we can rewrite the above equation as

$$
f_\bt{X}(\bt{x}) = \frac{1}{2\pi \sigma_x \sigma_y }\textrm{exp}\bigg\{-\frac{1}{2}(\bt{x} - \bt{\mu})^T\Sigma^{-1}(\bt{x} - \bt{\mu})\bigg\}\\
$$

Intuitively, this makes sense: the smaller the variance of some random variable $X_i$
, the more “tightly” peaked the Gaussian distribution in that dimension.

Till now we only discussed a multivariate normal distribution where each random variable is independent (contour axes are aligned with co-ordinate axes). But what if the two random variables $X$ and $Y$ are not independent ($\cov(X, Y) != 0$). In that case, the contours are still elliptical, but their major and minor axes are not aligned with the coordinate axes.

![multivariate_normal](/assets/images/probability/further_topics.assets/multivariate_normal.png)

How do we derive the equation for this distribution? Does the last equation still hold? For this we consider $\bt{X}$, such that $\bt{X_1}, \dots, \bt{X_n}$ are independent normal variables and apply a linear transform to $\bt{X}$. Then we derive the distribution for this transformed random variable. 

In our case, the affine transformation will consist of a rotation followed by a scaling along the principal axes of our rotation, with one translation. Let the affine transformation function be $L: \mathbb{R}^N \to \mathbb{R}^N$, such that $L(\bt{x}) = \bt{Ex} + \bt{b}$. Here $\bt{E}$ can be represented as the square root of a symmetric positive definite matrix. If $\Delta = \bt{U}\Lambda\bt{U}^T$ is the symmetric positive definite matrix, then $\bt{E} = \Delta^{1/2} = \Lambda^{1/2}\bt{U}$. More details of matrix square root can be found [here](https://bookdown.org/compfinezbook/introcompfinr/Positive-Definite-Matrices.html). Our aim is to find the probability distribution for $\bt{Z} = L(\bt{X})$

We know the following things about $\bt{Z}$ :  
1. $\expect[Z] = \mu_Z = L(\expect[X]) = L(\mu_X)$
2. $\Sigma_\bt{Z} = \bt{E}\Sigma_\bt{X}\bt{E}^T$. 

Also, $\bt{x - \mu_x} = \bt{E}^{-1}(\bt{z - \mu_z})$. 

Substituting this in the equation for $f_\bt{X}$, we get  

$$
\begin{align}
f_\bt{Z}(\bt{z}) &= k\,\textrm{exp}\bigg\{-\frac{1}{2}\big[\bt{E}^{-1}(\bt{z - \mu_z})\big]^T\Sigma_\bt{X}^{-1}\bt{E}^{-1}(\bt{z - \mu_z})\bigg\} \\  
&= k\,\textrm{exp}\bigg\{-\frac{1}{2}(\bt{z} - \mu_z)^T\Sigma_\bt{Z}^{-1}(\bt{z} - \mu_z)\bigg\} \\  
\end{align}
$$


