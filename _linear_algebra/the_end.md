---
layout: default
item_num: 6
title: The End
slug: the-end
---

$
\newcommand{\mat}[1]{\begin{bmatrix} #1 \end{bmatrix}}
\newcommand{\bt}[1]{\mathbf{#1}}
$

## Linear Transformations and their Matrices 

*This is majorly a copy of the scribe note for [Lecture 30](https://ocw.mit.edu/courses/mathematics/18-06sc-linear-algebra-fall-2011/positive-definite-matrices-and-applications/linear-transformations-and-their-matrices/MIT18_06SCF11_Ses3.6sum.pdf) of MIT OCW 18.06*

<p><!--excerpt-->So after having discussed Eigenvectors and Singular Value Decomposition, Strang decides to discuss Linear Transformations. The same linear transformations that were discussed right at the beginning of "Essence of Linear Algebra" (leading to the very definition of Matrix Multiplication). The lecture basically goes through the same ideas but Strang does a rather good job of putting forward the same ideas.<!--excerpt--></p>

First, we discuss linear transformations without any underlying grid (without co-ordinates). Transformation of a vector is a translation of the vector from one position to the other. A transformation $T$ is linear if it follows the following two properties:
1. $T(\bt{v}+\bt{u}) = T(\bt{v}) + T(\bt{u})$
2. $T(c\bt{v}) = cT(\bt{v})$

It’s worth noticing that $T(\bt{0}) = \bt{0}$, because if not we can't have $T(c\bt{0}) = cT(\bt{0})$. The point representing the tip of $\bt{0}$ is the origin. All vectors can be thought of as originating at the origin.

**Example of non-linear transformation:** Shifting all the vectors by a constant vector $\bt{v_0}$.<!--excerpt--> 

$T(\bt{v}) = \bt{v} + \bt{v_0}$

Here $T(2\bt{v}) = 2\bt{v} + \bt{v_0} \neq 2T(\bt{v})$. Thus $T$ is not a linear transformation

**Example of a linear transformation:** Rotation by $45^o$

This transformation $T : \mathbb{R}^2 → \mathbb{R}^2$ takes an input vector $\bt{v}$ and outputs the vector $T(\bt{v})$ that comes from rotating v counterclockwise by $45^o$ about the origin. Note that we can describe this and see that it is linear without using any coordinates. 



One advantage of describing transformations geometrically is that it helps us to see the big picture, as opposed to focusing on the effect of the transformation on a single point. We can quickly see how rotation by $45^o$ will transform a picture of a house in the plane. If the transformation was described in terms of a matrix rather than as a rotation, it would be harder to guess what the house would be mapped to. 



Now we introduce a grid in the space and bring matrices into the picture. Each vector now is represented by a set of co-ordinates (with respect to standard basis). Observe that multiplying a vector with a matrix leads to a linear transformation of the vector, as the multiplication follows both the rules of linearity.  

How do we describe a linear transformation with the help of this grid? We saw that a matrix multiplication is a linear transformation. Can each linear transformation be represented by a matrix?  

How much information is needed to know $T(\bt{v})$ for all possible inputs? We get input $\bt{v_1}$ and we return $T(\bt{v_1})$. We get input $\bt{v_2}$, we return $T(\bt{v_2})$. With this we can automatically find out the linear transformations for all linear combinations of $\bt{v_1}$ and  $\bt{v_2}$, using laws of linearity. Therefore, if we know the linear transformations for a set of basis vector, we can find out the transform for any other vector in space. Let $\bt{v_1} \dots \bt{v_n}$ be basis vectors, then any $\bt{v}$ can be expressed as 

$$
\begin{align}
\bt{v} &= c_1\bt{v_1} + c_2\bt{v_2} + c_3\bt{v_3} + \dots + c_n\bt{v_n} \\
\implies T(\bt{v}) &= c_1T(\bt{v_1}) + c_2T(\bt{v_2}) + c_3T(\bt{v_3}) + \dots + c_n\bt{v_n}
\end{align}
$$

Thus $A = [T(\bt{v_1}),T(\bt{v_2}),\dots,T(\bt{v_n})]$ can describe, in entirety, any linear transformation $T$ on $\mathbb{R}^n$. 

We can also see that in order to get the linear transform of $\bt{v}$ (denoted by $T(\bt{v})$), we need to take a linear combination of the columns of $A$ scaled by the same scaling factors used to obtain $\bt{v}$ from standard basis. Thus,

$$
T(\bt{v}) = A\bt{v}
$$

**Conclusion**

For any linear transformation $T$ we can find a matrix $A$ so that $T(\bt{v}) = A\bt{v}$. If the transformation is invertible, the inverse transformation has the matrix $A^{−1}$. The product of two transformations $T_1 : \bt{v} → A_1\bt{v}$ and $T_2 : \bt{w} → A_2\bt{w}$ corresponds to the product $A_2 A_1$ of their matrices. This is where matrix multiplication comes from!