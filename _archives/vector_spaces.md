---
layout: default
title: Vector Spaces
slug: vectors
item_num: 1
excerpt: This is meant to accompany each corresponding video in the Essence of Linear Algebra Series. Here we study the first eight chapters of the series. These notes are meant as an index (with some additional commentary) for the topics covered in the vidoes and are not meant as a substitute for the videos.
---

$$
\newcommand{\mat}[1]{\begin{bmatrix} #1 \end{bmatrix}}
\newcommand{\bt}[1]{\mathbf{#1}}
$$

# Vector Spaces

*This is meant to accompany each corresponding video in the Essence of Linear Algebra Series. Here we study the first eight chapters of the series. These notes are meant as an index (with some additional commentary) for the topics covered in the vidoes and are not meant as a substitute for the videos.*



### What are Vectors?

Is it a list of numbers (CS student perspective)? Is it an arrow in space with a length and direction and that can be moved around in space (physics student perspective)? We define it with a Maths perspective. For a maths student, it is anything for which the two operations, vector addition and scalar multiplication, make sense.



### Linear Combinations, Span and Basis Vectors

What is a Linear Combination of two vectors? Any time you scale two vectors and then add them together, it is called a linear combination of the two vectors. All vectors that can be obtained by taking linear combinations of a set of vectors constitute the **span** of the given set of vectors. A set of vectors in which addition and scalar multiplication are closed operations, is called a **vector space**. All spans constitute a vector space.

Suppose we have a set of vectors. If adding another vector doesn’t add anything to the span of the original vectors, then the added vector is a linear combination of the original vectors. On the other hand, if the newly added vector adds more vectors to the span of the previous set, then the new vector is said to add a dimension to the span. A set of vectors is said to be **Linearly Independent**, if no one particular vector can be obtained by linearly combining the rest of the vectors in the set.

The **basis** of a vector space is a set of linearly independent vectors that span the full space. Every co-ordiante system uses a set of basis vectors to assign co-ordinates to each vector. The co-ordinates of a given vector represent the amount by which each basis vector needs to be scaled, in order to obtain the given vector. Each time we represent a vector numerically, we make an implicit choice of the basis vectors to be used. $\hat{\bt{i}} $  , $\hat{\bt{j}} $   and $\hat{\bt{k}} $  are the basis vectors of the standard co-ordinate system. They are unit vectors (vectors with length $1$). The number of vectors in the basis of a vector space is the **dimension** of the vector space. Now we know that each vector space can have infinitely many basis sets. Do all of these basis sets have the same number of vectors? Yes! [Proof $\mid$ Khan Academy](https://www.khanacademy.org/math/linear-algebra/vectors-and-spaces/null-column-space/v/proof-any-subspace-basis-has-same-number-of-elements)

Similar line of reasoning can also be used to prove that if $\bt{V}$  is a subspace of $\mathbb{R}^n$ with dimension $n$, then $\bt{V} = \mathbb{R}^n$. If $\bt{V} \subsetneqq \mathbb{R}^n$, then we need to add a few vectors from basis($\mathbb{R}^n$) to basis($\bt{V}$), in order to span the full space of $\mathbb{R}^n$. The basis that we get in this way will have more than $n$ vectors. But we just saw that all the different basis sets of a vector space have the same number of vectors. Hence, $\bt{V} = \mathbb{R}^n$. This also proves that there can be atmost $n$ independent vectors in $\mathbb{R}^n$.



### Linear Transformations and Matrices

What is a transformation? It is a function that maps every input vector of a vector space to an output vector. You can visualize a transformation as taking every vector in a vector space and *moving* it to a new vector. Visualizing so many vectors moving all at once can be a bit tricky. For simplicity, we can represent each vector by a point sitting at the tip, and then visualize the points (tips) moving from one location to the other, instead of the entire vectors. Further, instead of looking at the movement of all the points, it is more intuitive to only look at the points on the gridlines.

Linear Algebra is limited to the study of *Linear* Transformations. What are *Linear* Transformations? You can think of a linear transformation as arbitrarily moving unit vectors to different locations, and then the locations of all other vectors $\bt{x}$ are determined as follows:

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


$$
(f\circ g)(\bt{x}) = a(f\circ g)({\hat{\bt{i}}}) + b(f\circ g)({\hat{\bt{j}}})
$$


Thus the Composite Linear Transformation ($f\circ g$) can be expressed in the matrix form.  How do we find the matrix representing $(f\circ g)$? The same way we find the matrix for any other linear transform. We track where the unit vectors land after the two consecutive transformations and then represent them as columns of a matrix.

How do we apply two consecutive transformations, first $$G = \mat{\bt{g_1} & \bt{g_2}}$$ and then $F = \mat{\bt{f_1} & \bt{f_2}}$? We first take the unit vectors $\hat{\bt{i}}, \hat{\bt{j}}$ to $\hat{\bt{i'}} = \bt{g_1}, \hat{\bt{j'}} = \bt{g_2}$. To apply the second transformation, we move $\hat{\bt{i}}, \hat{\bt{j}}$ to $\bt{f_1}, \bt{f_2}$. Notice that $\hat{\bt{i'}}, \hat{\bt{j'}}$ are not the vectors being moved to $\bt{f_1}, \bt{f_2}$! Why? Because the columns of a matrix represent where the basis vectors of the co-ordinate system land. The co-ordinates of $\hat{\bt{i'}}, \hat{\bt{j'}}$ are with respect to the basis $\{\hat{\bt{i}}, \hat{\bt{j}}\}$.

The matrix representing the overall transform will be as follows :

$$
\begin{align}
& \mat{\hat{\bt{i''}} & \hat{\bt{j''}}} \\
= & \mat{f(\hat{\bt{i'}}) & f(\hat{\bt{j'}})} \\
= & \mat{f(g(\hat{\bt{i}})) & f(g(\hat{\bt{j}}))} \\
= & \mat{f(\bt{g_1}) & f(\bt{g_2})} \\
= & \mat{F\bt{g_1} & F\bt{g_2}}
\end{align}
$$

This is the definition of matrix multiplication : 

$$
FG = \mat{\bt{f_1} & \bt{f_2}}\mat{\bt{g_1} & \bt{g_2}}= \mat{F\bt{g_1} & F\bt{g_2}}
$$



### The Determinant

A Determinant represents the number by which the area/volume of the unit square/cube is squished or stretched after a 2-D/3-D transformation. Because all the gridlines remain parallel and equidistant after the linear transformation, all unit squares/cubes are squished or stretched by the same degree. Also, any area/volume in the plane/space can be thought of as being made up of many infinitesimal squares/cubes. Thus any area/volume is also squished/stretched by the same amount, given by the determinant of the transformation. 

 The value of the determinant is (-ve) if the orientation of the grid has been flipped by the transformation. Negative value of the determinant can be visualized as the area of unit square slowly reducing to zero and then increasing on the other side of orientation of X-axis and Y-axis.  

The intuition given here makes it almost trivial to prove that $\textrm{det}(AB) = \textrm{det}(A)\textrm{det}(B)$.



### Inverse Matrices, Column Space and Null Space

Matrices are mostly used to solve systems of linear equations. The process to do this is Gaussian Elimination and Row Echelon Form which we discuss in the coming note. Here we discuss the intuition behind this method of solving linear equations. In this section we consider only square matrices (number of equations is equal to the number of unknowns). 

A set of linear equations can be represented as $A\bt{x} = \bt{b}$. In order to solve this equation, we need to find the vector $\bt{x}$ that lands on $\bt{b}$ after the transformation is applied to it. If a matrix multiplication doesn’t squish the space ($\textrm{det}(A)\neq 0$), then for every $\bt{b}$ we can find a solution $\bt{x}$. How do we find this $\bt{x}$? By playing the transformation in reverse. $A^{-1}$ denotes the inverse transformation of $A$. It brings back each vector to exactly where it was before the transformation. This new matrix is known as the inverse of $A$. Using this inverse, the solution can be written as $\bt{x} = A^{-1}\bt{b}$.

The case where the transformation squishes the space (the determinant is zero) is more complicated. No function can un-squish the space (inverse matrix doesn't exist). We may still get a solution but for that we need to be lucky. The vector $\bt{b}$ needs to lie in the squished space.

Rank of a matrix is defined as the dimension of the column span. It is obvious that it is the number of independent columns in the transformation matrix. Our next note describes what pivot columns are and how the rank is equal to the number of pivot columns.

The corresponding video also helps get an intuitive understanding of why 

<center><b> rank(column space) + rank(null space) = n </b></center>

### Nonsquare matrices as transformations between dimensions

A $2\times 2$  matrix transforms one 2D vector into another 2D vector. Similarly for a $3\times 3$ matrix. What about non-square matrices? Non-square matrices are transformations between dimensions. A $2\times 3$ matrix is a transformation that takes in a vector in 3D space and gives out a vector in 2D space. Thus it reduces the dimension by 1. Observe that this is not the same as a $3\times 3$ matrix that reduces the space to a flat plane. In the later case, the column space is a subset of $\mathbb{R}^3$, though the basis of column space has only two vectors.

A very important non-square matrix is the $1 \times 2$ matrix. It takes vectors in $\mathbb{R}^2$ and maps them onto a number line. This transformation has close ties to the dot product.

*After going through this note, study the chapters on "Dot Prodcut and Duality" and "Cross Products" in the Essence of Linear Algebra series. The two videos after that, namely,  "Cross products in the light of linear transformations" & "Cramer's rule, explained geometrically", fall outside the scope of essence of linear algebra. Go through them, only if needed.*