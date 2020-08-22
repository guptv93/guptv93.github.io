---
layout: default
title: Vector Spaces
slug: vectors
item_num: 1
---

$$
\newcommand{\mat}[1]{\begin{bmatrix} #1 \end{bmatrix}}
\newcommand{\bt}[1]{\mathbf{#1}}
$$



# Vector Spaces


*<!--excerpt-->This is meant to accompany each corresponding video in the Essence of Linear Algebra Series. Here we study the first eight chapters of the series. These notes are meant as an index (with some additional commentary) for the topics covered in the vidoes and are not meant as a substitute for the videos.<!--excerpt-->*


### What are Vectors?

Is it a list of numbers (CS student perspective)? Is it an arrow in space with a length and direction and that can be moved around in space (physics student perspective)? We define it with a Maths perspective. For a maths student, it is anything for which the two operations, vector addition and scalar multiplication, make sense.

The video also goes over vector addition and multiplication.  


### Linear Combinations, Span, and Basis Vectors

What is a Linear Combination of two vectors? Any time you scale two vectors and then add them together, it is called a linear combination of the two vectors.

Below is some terminology relating to linear combinations of vectors.

*Span:* All vectors that can be obtained by taking linear combinations of a set of vectors is the span of the particular set of vectors.

*Vector Space:* A set of vectors in which addition and scalar multiplication are closed operations. All spans constitute a vector space.

*Linear Independence:* Suppose we have a set of vectors. If adding another vector doesn’t add anything to the span of the original vectors, then the added vector is a linear combination of the original vectors. In this case, the set of vectors (original plus last added) are Linearly Dependent. On the other hand, if the newly added vector adds more vectors to the span of the previous set, then the new vector is said to add a *dimension* to the span.

*Basis Vectors:* The basis of a vector space is a set of linearly independent vectors that span the full space. Every co-ordiante system uses a set of basis vectors to assign co-ordinates to each vector. The co-ordinates of a given vector represent the amount by which each basis vector needs to be scaled, in order to obtain the given vector. Each time we represent a vector numerically, it depends on an implicit choice of the basis vectors we are using. $\hat{\bt{i}}$ and $\hat{\bt{j}}$ are the basis vectors of the standard co-ordinate system. They are unit vectors (vectors with length $1$).

*Dimension:* In the definition of Linear Independence, if the newly added vector adds more vectors to the span, then the new vector is said to add a dimension to the span. The number of vectors in the basis of a vector space is the dimension of the vector space. Now we know that each vector space can have infinitely many basis sets. Do all of these basis sets have the same number of vectors? Yes! [Proof $\mid$ Khan Academy](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/null-column-space/v/proof-any-subspace-basis-has-same-number-of-elements)  

Similar line of reasoning can also be used to prove that if $\bt{V}$  is a subspace of $\mathbb{R}^n$ with dimension $n$, then $\bt{V} = \mathbb{R}^n$. If $\bt{V} \subsetneqq \mathbb{R}^n$, then we need to add a few vector from basis($\mathbb{R}^n$) to basis($\bt{V}$), in order to span the full space of $\mathbb{R}^n$. However the basis that we get in this way will have more than $n$ vectors. We just proved that all the different basis sets of a vector space have the same number of vectors. Hence, $\bt{V} = \mathbb{R}^n$. This also proves that there can be atmost $n$ independent vectors in $\mathbb{R}^n$.


### Linear Transformations and Matrices

What is a transformation? It is a function that maps every input vector of a vector space to an output vector. You can visualize a transformation as taking every vector in a vector space and *moving* it to a new vector. Visualizing so many vectors moving all at once can be a bit tricky. For simplicity, we can represent each vector by a point sitting at the tip, and then visualize the points (tips) moving from one location to the other, instead of the entire vectors. Further, instead of looking at the movement of all the points, it is more intuitive to only look at the points on the gridlines.

Linear Algebra is limited to the study of *Linear* Transformations. What are *Linear* Transformations? You can think of a linear transformation as arbitrarily moving unit vectors to different locations, and then the locations of all other vectors $\vec{x}$ are determined as follows:

$$
\begin{align}
\bt{x} &= a\hat{\bt{i}} + b\hat{\bt{j}} \\
f(\bt{x}) &= af(\hat{\bt{i}}) + bf(\hat{\bt{j}}) & f\text{ is a linear transformation of vector space}
\end{align}
$$

Because of the above mentioned property, it is obvious that the grid lines remain (firstly linear,) parallel and equidistant from each other during a linear transformation. Why? Because suppose $\hat{\bt{i}}, \hat{\bt{j}}$ are moved to $\hat{\bt{i'}}, \hat{\bt{j'}}$, then the new distance between points $(1,0)$ and $(2,0)$ will be equal to that between points $(2,0)$ and $(3,0)$ (both being equal to $\|\hat{\bt{i'}}\|$) and so on. A transformation of a vector space is a linear transformation if and only if the new grid lines are still parallel and equidistant from ech other.

A matrix is a horizontal list of vectors. Matrix helps us concisely denote a linear transformation of space. It lists the new locations of the unit vectors after the transformation. Multiplying a vector with a matrix gives the transformed vector.

Multiplying a vector with a matrix can be thought of denoting a linear combination of the column vectors of the matrix. Each column vector is first scaled by the corresponding row entry in the vector and then all these scaled column vectors are added. Thus, if $\bt{x}$ started off as a linear combination of the unit vectors $\hat{\bt{i}}, \hat{\bt{j}}$, then after the transformation it ends up being the same linear combination of the transformed unit vectors $\hat{\bt{i'}}, \hat{\bt{j'}}$.  

Another way of thinking about Linear Transformation (apart from moving all vectors in the vector space) is in terms of change of the co-ordinate system. Instead of moving each point, we just give each point different coordinates. Multiplying by the transformation matrix takes us from the new coordinate system to the old coordinate system. This is discussed further under the topic "Change of Basis".

### Matrix Multiplication as Composition

Many a times we want to sequentially apply multiple transformations to a vector space, one after the other. This is called a Composition of Linear Transformations. It is easy to understand why a composition of linear transformations will be a linear transformation all in itself (the gridlines will still be parallel and the origin would not have moved). Also, if $g$ and $f$ are the first and second linear transformations, then it is obvious that:

$$(f\circ g)(\bt{x}) = a(f\circ g)({\hat{\bt{i}}}) + b(f\circ g)({\hat{\bt{j}}})$$

Thus the Composite Linear Transformation ($f\circ g$) can be expressed in the matrix form.  How do we find the matrix representing $(f\circ g)$? The same way we find the matrix for any other linear transform. We track where the unit vectors land after the two consecutive transformations and then represent them as columns of a matrix.

How do we apply two consecutive transformations, first $G = [\bt{g_1}, \bt{g_2}]$ and then $F = [\bt{f_1}, \bt{f_2}]$? We first take the unit vectors $\hat{\bt{i}}, \hat{\bt{j}}$ to $\hat{\bt{i'}} = \bt{g_1}, \hat{\bt{j'}} = \bt{g_2}$. To apply the second transformation, we move $\hat{\bt{i}}, \hat{\bt{j}}$ to $\bt{f_1}, \bt{f_2}$. Notice that $\hat{\bt{i'}}, \hat{\bt{j'}}$ are not the vectors landing on $\bt{f_1}, \bt{f_2}$; $\hat{\bt{i}}, \hat{\bt{j}}$ are! Why? Because the columns of a matrix represent where the basis vectors of the co-ordinate system land. The co-ordinates of $\hat{\bt{i'}}, \hat{\bt{j'}}$ are with respect to the [basis](https://en.wikipedia.org/wiki/Basis_(linear_algebra)) $\{\hat{\bt{i}}, \hat{\bt{j}}\}$.

The matrix representing the overall transform will be as follows :

$$
\begin{align}
& [\hat{\bt{i''}}, \hat{\bt{j''}}] \\
= & [f(\hat{\bt{i'}}), f(\hat{\bt{j'}})] \\
= & [f(g(\hat{\bt{i}})), f(g(\hat{\bt{j}}))] \\
= & [f(\bt{g_1}), f(\bt{g_2})] \\
= & [F\bt{g_1}, F\bt{g_2}]
\end{align}
$$

This is the definition of matrix multiplication : $FG = [\bt{f_1}, \bt{f_2}][\bt{g_1},\bt{g_2}] = [F\bt{g_1}, F\bt{g_2}]$.

### Three Dimensional Linear Transformations

This video goes over linear transformations in 3D space instead of a 2D plane.


### The Determinant

A Determinant represents the number by which the unit square/cube is squished or stretched after a 2-D/3-D transformation. The value of the determinant is (-ve) if the orientation of the grid has been flipped by the transformation. Negative value of the determinant can be visualized as the area of unit square slowly reducing to zero and then increasing on the other side of orientation of X-axis and Y-axis.  

The intuition given here makes it almost trivial to prove that $\textrm{det}(AB) = \textrm{det}(A)\textrm{det}(B)$.


### Inverse Matrices, Column Space and Null Space

Matrices are mostly used to solve systems of linear equations. The process to do this is Gaussian Elimination and Row Echelon Form which we discuss in the coming note. Here we discuss the intuition behind this method of solving linear equations. In this section we consider only square matrices (number of equations is equal to the number of unknowns). 

A set of linear equations can be represented as $A\bt{x} = \bt{b}$. In order to solve this equation, we need to find the vector $\bt{x}$ that lands on $\bt{b}$ after the transformation is applied to it. If a matrix multiplication doesn’t squish the space ($\textrm{det}(A)\neq 0$), then for every $\bt{b}$ we can find a solution $\bt{x}$. How do we find this $\bt{x}$? By playing the transformation in reverse. $A^{-1}$ denotes the inverse transformation of $A$. It brings back each vector to exactly where it was before the transformation. This new matrix is known as the inverse of $A$. Using this inverse, the solution can be written as $\bt{x} = A^{-1}\bt{b}$.

The case where the transformation squishes the space (the determinant is zero) is more complicated. No function can un-squish the space (inverse doesn't exist). We may still get a solution but for that we need to be lucky. The vector $\bt{b}$ needs to lie in the squished space.

Rank of a matrix is defined as the dimension of the column span. It is obvious that it is the number of independent columns in the transformation matrix. Our next note describes what pivot columns are and how the rank is equal to the number of pivot columns.

The video also helps get an intuitive understanding of why rank(column space) + rank(null space) = n.  


### Nonsquare matrices as transformations between dimensions

A $2\times 2$  matrix transforms one 2D vector into another 2D vector. Similarly for a $3\times 3$ matrix. What about non-square matrices? Non-square matrices are transformations between dimensions. A $2\times 3$ matrix is a transformation that takes in a vector in 3D space and gives out a vector in 2D space. Thus it reduces the dimension by 1. Observe that this is not the same as a $3\times 3$ matrix that reduces the space to a flat plane. In the later case, the column space is a subset of $\mathbb{R}^3$, though the basis of column space has only two vectors.

A very important non-square matrix is the $1 \times 2$ matrix. It takes vectors in $\mathbb{R}^2$ and maps them onto a number line. This transformation has close ties to the dot product.

### Dot Products and Duality

First, we study the meaning of a dot product. Dot product of $\bt{u}$ and $\bt{v}$ denotes $\|\textrm{proj}_\bt{v}\bt{u}\|\|\bt{v}\|$. From the definition, it feels odd that dot product of $\bt{u}$ and $\bt{v}$ is the same as dot product of $\bt{v}$ and $\bt{u}$. The video gives the intuition to why $\bt{u}\cdot\bt{v} = \bt{v}\cdot\bt{u}$.  

Now for 2D vectors, $\bt{u} \cdot \bt{v} = u_xv_x + u_yv_y$. To understand the derivation of this formula, we need to understand duality. The Duality property has been stated below. See the video for its explanation.

**Duality**
Any vector $\bt{u} = \mat{u_x \\ u_y}$ can be looked at as a matrix $\mat{u_x&u_y}$ which transforms 2D space into 1D space.  Projection of $\bt{v}$ on $\bt{u}$ can be thought of as the linear transformation of $\bt{v}$ by the above matrix ($\bt{u}^T$), given $\bt{u}$  is a unit vector.    

This property of Duality, of seeing every projection as a linear transformation from 2D to 1D, is what leads to the derivation of dot product as elementwise vector multiplication $(\bt{u} \cdot \bt{v} = u_xv_x + u_yv_y)$.


### Cross Products

The cross product of two vectors $\bt{u},\bt{v}$ (denoted as $\bt{u}\times\bt{v}$) is another vector that is perpendicular to the plane formed by $\bt{u}$ and $\bt{v}$ and whose length is equal to the area of the parallelogram formed by $\bt{u}$ and $\bt{v}$.  

$\|\bt{u}\times\bt{v}\| = \textrm{det}(\mat{\bt{u}&\bt{v}})$
$\bt{u}\times\bt{v} = - \bt{v}\times\bt{u}$



*The next two videos "cross products in the light of linear transformations" & "cramer's rule, explained geometrically", fall outside the scope of essence of linear algebra. Go through them, only if needed. Otherwise knowing how to calculate the cross product and how to solve equations using Cramer's rule suffices.*

