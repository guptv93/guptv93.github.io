---
layout: default
title: Transformations
slug: transform
item_num: 4
---

# Transformations

### Linear Transformations of Random Variables
<p><!--excerpt-->Given the PDF of a random variable $X$, how do you get the PDF of a derived random variable <!--excerpt--> $2X+1$. It is very simple. The probability of any value $x$ will now be the probability of $2x+1$. Therefore, the entire PDF is stretched (horizontally) to twice its size, and then translated horizontally to the right by $1$ unit.</p>

![image-20200628161957719](/assets/images/probability/transformations.assets/image-20200628161957719.png)

$$
\bigg\Downarrow
$$

![image-20200628162344123](/assets/images/probability/transformations.assets/image-20200628162344123.png)

Notice that the area under the graph is constant (total probability over $\mathbb{R}$ is $1$). Therefore, if the graph is stretched horizontally, then it will be shrinked vertically.



### Linear Transformations of Functions

Now let us talk about general functions. If we are given the graph of $f(x)$, how do we derive the graph of $g(x) = f(2x+1)$? Do we follow the same procedure that we used to plot the PDF of a linear transformation of a random variable? Notice here that the new value mapped to $2x+1$ (by $g$) isn't equal to the value that was mapped to $x$ previously (by $f$). Rather $x$ is now assigned the value that was assigned to $2x+1$ previously. If we refer to $2x+1$ as $x_{prev}$, then

$$
\begin{align}
&2x + 1 = x_{prev}\\
\implies &x = \frac{x_{prev}-1}{2} \\
\textrm{and } &g(\frac{x_{prev}-1}{2}) = f(x_{prev})
\end{align}
$$

The value that was initially assigned to $x_{prev}$ (by $f$) is now assigned to $\frac{x_{prev}-1}{2}$ (by $g$). Thus, to derive the graph of $g$, we first translate the graph of $f$ to the left by $1$ unit and then shrink it to half.  

![image-20200628161957719](/assets/images/probability/transformations.assets/image-20200628161957719.png)

$$
\bigg\Downarrow
$$

![image-20200628162518377](/assets/images/probability/transformations.assets/image-20200628162518377.png)

**Another Example:**

We are given the plot for $F(x) = x^2$ and we need to plot $G(y) = F(2-2y) = (2-2y)^2$. $G$ takes the same value as $F$ (the value of the image/output), when:

$$
\begin{align}
&2-2y = x \\
\implies &y = \frac{2-x}{2} \\
\end{align}
$$

For any given $x$,  $F(x) = G(y)$, when $y = (2 - x)/2$. Thus, to transform plot of $F$ to the plot of $G$, we map every $x$ to $(2-x)/2$. We first reflect the graph of $F$ on Y-axis, shift the graph to the right by 2 units, and then shrink the graph horizontally by a factor of $2$.

**Alternate Explanation:**

Let me try to explain the same thing differently. If we want to plot the function $f$, we plot the value of $x$ on X-axis and the value of $f(x)$ on Y-axis. How do we find $f(3-x)$? For each value of $x$, we plot what value is assigned by $f$ to $3-x$. Let us call this new function $g$ ($g(x) =f(3-x)$), for convenience sake.

Given a value of $x$, to get the value $3-x$ we reflect $x$ on Y-axis and then shift it by $3$ units to the right. Let us call this new point $x_{prev}$. Whatever value $f$ assigns to $x_{prev}$, will be assigned by $g$ to the point $x$. Therefore, if we take any $x_{prev}$, and do the exact opposite operations (first shift left by $3$, then reflect on Y-axis) we get to a point $x$ such that $g(x) = f(x_{prev})$. Thus, by shifting the graph of $f(x)$ to left by $3$ and then reflecting it on Y axis, we get the graph of $g(x)$ or $f(3-x)$.