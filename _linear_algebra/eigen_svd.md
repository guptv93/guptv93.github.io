---
layout: default
title: EigenDecomposition and SVD
slug: eigen-svd
item_num: 5
---

$$
\newcommand{\mat}[1]{\begin{bmatrix} #1 \end{bmatrix}}
\newcommand{\bt}[1]{\mathbf{#1}}
$$



# EigenDecomposition and SVD

*<!--excerpt-->In the last note, we looked at our first application of Linear Algebra in Machine Learning. Here we look at SVD, which again has lots of applications in Machine Learning, one of the most common being PCA. We will close our study of Linear Algebra with the introduction of SVD. We will introduce the applications of SVD (and Linear Algebra in general) to Machine Learning in another series.<!--excerpt-->*



### Change of Basis
We all share the same Space and look at the same vectors. However we use different languages to describe the vectors. These languages are called co-ordinate systems. Each co-ordinate system has its own set of basis vectors, based on which it assigns unique co-ordinates to each vector. All the languages agree on only one thing. The location of the origin $(0,0)$, where a vector lands if you scale if by $0$. The standard co-ordinate system ($\mathbb{C}$) in 2D uses $\hat{\bt{i}}, \hat{\bt{j}}$ as basis vectors. This is written as $\mathbb{C}=\langle\hat{\bt{i}},\hat{\bt{j}}\rangle$.

How do the co-ordinates of a vector change when we change the basis vectors (co-ordinate system)? Let $A$ be the matrix whose columns are the basis vectors of co-ordinate system $\mathbb{C}'$. Multiplying $\bt{x}$ (in $\mathbb{C}$) by $A$, we get $\bt{b}$ (in $\mathbb{C}$). This $\bt{b}$ (in $\mathbb{C}$) is the same as $\bt{x}$ (in $\mathbb{C}'$), because you are scaling the basis vectors of $\mathbb{C}'$ by the elements of $\bt{x}$. Thus, to convert the coordinates of any $\bt{x}$ (in $\mathbb{C}'$) to the co-ordinate system $\mathbb{C}$, we multiply $\bt{x}$ by the matrix $A$ (such that the columns of matrix $A$ represent the basis vectors of $\mathbb{C}'$).

Thus, if I want to use a co-ordinate system with $\mat{\bt{u_x}&\bt{u_y}&\bt{u_z}}$ as basis vectors, then the co-ordinates of $\bt{x}$ in the new co-ordinate system are given by $\mat{\bt{u_x}&\bt{u_y}&\bt{u_z}}^{-1}\bt{x}$.  

Another way of looking at this is $\mat{\bt{u_x}&\bt{u_y}&\bt{u_z}}\mat{\bt{u_x}&\bt{u_y}&\bt{u_z}}^{-1}\bt{x} = \bt{x}$. Thus, $\mat{\bt{u_x}&\bt{u_y}&\bt{u_z}}^{-1}\bt{x}$ is the representation of $\bt{x}$ when basis vectors are $\bt{u_x},\,\bt{u_y},\,\bt{u_z}$.

This concept is quintessential for a good understanding of Eigendecomposition and SVD. Watch 3Blue1Brown's video on  [change of basis](https://youtu.be/P2LTAUO1TdA?t=537) for an in-depth explanation.



### Eigenvectors and Eigenvalues
There might be some vectors during a linear transformation, that only get stretched or squished (and don't change their direction). Scalar multiples of such vectors will also have the same property of not changing their direction. Such vectors are called the eigenvectors of a transformation. The factor by which an eigenvector is stretched or squished is called the eigenvalue of that eigenvector.  

If $\bt{v}$ is the eigenvector for a transformation $A$, and the corresponding eigenvalue is $\lambda$, then 
$$A\bt{v} = \lambda\bt{v}$$
$$\implies(A - I\lambda)\bt{v} = \bt{0}$$

If $\textrm{det}(A - \lambda I) \neq 0$, then $\bt{v} = \bt{0}$ is the only solution of the above equation. Therefore eigenvectors exist only if $\textrm{det}(A - \lambda I) = 0$.  

Thus, the method of finding eigenvectors is as follows:
* Find $\lambda$ by solving the equation $\textrm{det}(A - \lambda I) = 0$.
* Sequentially plug in each value of $\lambda$ and derive the matrix $(A - I\lambda)$.
* Solve $(A - I\lambda)\bt{v} = \bt{0}$ to find $\vec{v}.$

Remember a linear transformation doesn't always have an eigenvector. For example, the rotation operation doesn't have any eigenvectors. Shear transformation $M = \mat{1&1\\0&1}$ has a single eigenvalue ($1$). A linear transformation that scales every vector by $2$, has a single eigenvalue ($2$), but has infinitely many eigenvectors in each direction.  

Suppose $P$ is the matrix of a projection onto a plane. For any $\bt{x}$ in the plane $P\bt{x} = \bt{x}$, so $\bt{x}$ is an eigenvector with eigenvalue $1$. A vector $\bt{x}$ perpendicular to the plane has $P\bt{x} = \bt{0}$, so this is an eigenvector with eigenvalue $\lambda = 0$. The eigenvectors of $P$ span the whole space (but this is not true for every matrix).

If the basis vectors are themselves eigenvectors of some transformation, then the transformation is represented by a diagonal matrix. In a diagonal matrix, only the elements on the principal diagonal are non-zero. We see that calculating higher powers of a diagonal matrix is trivial. But, we'll be rarely so lucky to have our basis vectors also be the eigen-vectors. How do we calculate higher powers for matrices whose eigenvectors are not the basis vectors? If the matrix is such that its eigenvectors span the whole space, then we can change choose the eigenvectors to be our basis vectors and change our co-ordinate system accordingly. This is known as the eigen-basis. In this eigen-basis system, the transformation only linearly scales each component. Therefore applying the same transformation multiple times is very easy. Finally when we have applied the transformation, we can convert back to our original coordinate system. 

Let $A$ be the matrix whose transformation we are interested in and whose eigenvectors span the entire space. Let $V$ be the matrix whose columns are the eigen-basis vectors. For any vector $\bt{x}$, $V^{-1}\bt{x}$ gives us the coordinates of $\bt{x}$ in eigen-basis. How would the transform represented by $A$ look in the eigen-basis system? It would only linearly scale each eigenvector of $A$, so it should be represented by a diagonal matrix $\Lambda$ in eigen-basis. $\Lambda^k V^{-1} \bt{x}$ gives the eigen-basis coordinates of $\bt{x}$ after applying the transform $k$ times. Now finally we want to convert these coordinates into our original basis. Thus the final vector in the original system is $V\Lambda^k V^{-1}\bt{x}$. From this we can conclude that $A = V\Lambda^k V^{-1}$ 

Watch 3Blue1Brown's video on  [eigenvectors and eigenvalues](https://www.youtube.com/watch?v=PFDu9oVAE-g) for an in-depth explanation.



### Eigenvalue Decomposition

The eigendecomposition is one form of matrix decomposition. Decomposing a matrix means that we want to find a product of matrices that is equal to the initial matrix. In the case of the eigendecomposition, we decompose the initial matrix into the product of its eigenvectors and eigenvalues. 

The pre-requisite for eigendecomposition of a matrix $A$ is that $A$ should have enough eigenvectors to span the entire space. In that case, we can use the eigenvectors of $A$ as the basis vectors of our new co-ordinate system. Notice that the columns of $A$ don't necessarily span full space (eigenvectors of $A$ do). A vector that belongs to the null-space of $A$ is also an eigenvector with $\lambda = 0$.

Let us construct a matrix $V$, such that $V$ is a square matrix with each column being an independent eigenvector of $A$. Also let $\Sigma$ represent the diagonal matrix whose diagonal values are the eigenvalues of the corresponding columns of $V$. As explained above, we can write 

$$
A = V\Sigma V^{-1}
$$

**Powers of a Matrix**

We use $A^2$ to denote application of the transform denoted by $A$ twice ($AA$). In general, it is a very difficult task to compute $A^k$ (for large $k$) even for small matrices. Eigenvalue Decomposition gives us a very easy way of doing the same. If we can write $A$ as $V\Sigma V^{-1}$, then 

$$
A^k = (V\Sigma V^{-1}) (V\Sigma V^{-1}) \dots(V\Sigma V^{-1}) = V\Sigma^kV^{-1}
$$

This equation intuitively makes sense. Once you shift a vector for normal basis to eigen-basis, repeated application of the transform just scales each component (along each eigenvector) repeatedly by the corresponding eigenvalue.



### Symmetric and Positive Definite Matrices

Let $S$ denote a square symmetric matrix. Notice that symmetric matrices are not always invertible (they don't have trivial null spaces). For example ${\bt{0}_{n\times n}}$ is symmetric but not invertible. Identity matrix with some diagonal entries changed to zero is also symmetric but not invertible.

**Property (without proof):** If $S_{n\times n}$ is a symmetric matrix, then it is possible to choose a set of $n$ eigenvectors that are orthogonal to each other.

We won't prove this property. Notice that $S$ doesn't exactly have to be invertible. If a vector $\bt{x}$ belongs to the null space of $S$, it is still an eigenvector with $\lambda = 0$.

Let $Q$ be the matrix whose columns are the orthonormal eigenvectors of $S$. Then

$$
\begin{align}
S &= Q\Lambda Q^{-1} \\
&= Q\Lambda Q^T &(Q^TQ = I)
\end{align}
$$

Let $Q$ have orthonormal unit column vector $\bt{q_1}, \bt{q_2}, \dots, \bt{q_n}$

$$
A = Q\Lambda Q^T = \mat{\bt{q_1}&\bt{q_2}&\dots}\mat{\lambda_1&&\\&\lambda_2&\\&&\ddots}\mat{\bt{q_1}^T\\\bt{q_2}^T\\\vdots} = \lambda_1\bt{q_1}\bt{q_1}^T + \lambda_2\bt{q_2}\bt{q_2}^T + \dots
$$

Remember, that if we want to find the projection of $\bt{p}$ on $\bt{a}$, we multiply $\bt{p}$ by the matrix $\frac{\bt{a}\bt{a}^T}{\bt{a}^T\bt{a}}$. $\bt{q_1}\bt{q_1}^T$ is the projection matrix for $\bt{q_1}$ as it is a unit vector. Also, all the columns of a projection matrix are scaled versions of the same vector. Thus a projection matrix is a rank one matrix! And from the equation above, every symmetric matrix can be decomposed as a linear combination of perpendicular projection
(rank one) matrix! This is known as the Spectral Theorem.

**Property (without proof): **Number of positive/negative eigenvalues for symmetric matrices can be determined from the signs of the pivots. The number of positive eigenvalues is the same as the number of positive pivots.

**Positive Definite Matrix:** A positive definite matrix is a symmetric matrix for which all eigenvalues are positive. A good way to tell if a matrix is positive definite is to check that all its pivots are positive. 

For a positive definite matrix $A$,

$$
\begin{align}
\bt{x}^TA\bt{x} &> 0 &(\forall \bt{x}, \bt{x}\neq \bt{0})
\end{align}
$$

This is easy to prove intuitively when you think of $A$ in terms of its Spectral Decomposition. $A\bt{x}$ gives us a vector whose projections on the orthogonal vectors $\bt{q_i}$ are linearly scaled in the same direction (positive eigenvalues). Therefore, when you take the dot product of $A\bt{x}$ and $\bt{x}$, all the elements along the various $\bt{q_i}$(s) will have a non-negative product and $\bt{x}^TA\bt{x} > 0$.

 $\bt{x}^TA\bt{x}$  is called a *quadratic form*. This quadratic form is always positive if $A$ is a positive definite matrix. More details about quadratic forms can be found [here](https://laurentlessard.com/teaching/cs524/slides/11 - quadratic forms and ellipsoids.pdf). 

Remember that an ellipse in 2D is given by

$$
\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1
$$

If $a > b$, then $a$ is called the semi-major axis. If $a < b$, then $b$ is the semi-major axis. If $a=b$, then the points form a circle with radius $a$. The equation for an ellipsoid in $n$ dimensions is:

$$
\frac{x_1^2}{a_1^2} + \frac{x_2^2}{a_2^2} + \cdots + \frac{x_n^2}{a_n^2} = 1
$$

The equations above represent ellipsoids whose axes coincide with the axes of the coordinate system. These equations can be represented in matrix lingo as $\bt{x}^T\Lambda\bt{x}$, where $\Lambda$ is a diagonal matrix. What if the axes of the ellipsoid don't fall on the axes of the coordinate system? Then the ellipsoid will be of the form $\bt{x}^TA\bt{x}$, where $A$ is positive definite. We know that $A=Q\Lambda Q^T$, where $Q$ is orthonormal and $Q^T = Q^{-1}$. If we perform change of basis to $Q$, then the equation again becomes $\bt{z}^T\Lambda \bt{z}$, where $\bt{z}$ are the coordinates in the eigen-basis. Thus $\bt{x}^TA\bt{x}$ represents an ellipsoid whose axes are along the eigenvectors of $A$.

Lec 6 (second half) of ECE-532 also covers Positive Definite Matrices and 3D ellipses.



### Prelude to SVD

First we study a couple of properties of the Positive Definite Matrices. If $A$ is positive definite, we denote it as $A\succ 0$.

**Property 1:** If $A\succ 0$ and $B \succ 0$, then $A+B \succ 0$.

Proof: 

$$
\begin{align}
\bt{x}^T(A+B)\bt{x} &= \bt{x}^TA\bt{x} + \bt{x}^TB\bt{x} > 0 &(\textrm{because } \bt{x}^TA\bt{x} > 0 \textrm{ and } \bt{x}^TB\bt{x} > 0)
\end{align}
$$

**Property 2:** If $A$ is a $m\times n$ matrix, then $A^TA$ is a symmetric positive definite matrix.

Proof:

$$
\bt{x}^T A^TA \bt{x} = (A\bt{x})^T(A\bt{x}) = \|A\bt{x}\|^2 \geq 0
$$

$\|{A\bt{x}}\| > 0$ is true only if $\bt{N}(A) = \{\bt{0}\}$. This is true if $\textrm{rank}(A) = n$.  

Finally we talk about Similar Matrices.

Two $n\times n$ matrices $A$ and $B$ are similar, if for some invertible matrix $M$

$$
A = MBM^{-1}
$$

Why do we call them similar? Because they have the same eigenvalues. 

$$
\begin{align}
& A\bt{x} = \lambda \bt{x}\\
\implies &MBM^{-1}\bt{x} = \lambda \bt{x} \\
\implies &BM^{-1}\bt{x} = \lambda M^{-1}\bt{x}
\end{align}
$$

Thus, $M^{−1}\bt{x}$ is an eigenvector of $B$ with the same eigenvalue.  

If $A$ has a full set of eigenvectors we can create its eigenvector matrix $S$ and write $S^{−1} A S = \Lambda$. So $A$ is similar to $\Lambda$. "Similarity" divides matrices into groups with identical set of eigenvalues. The most “preferable” of them, obviously, are diagonal matrices. They have trivial eigenvectors.  

When we **diagonalize** $A$, we’re finding a diagonal matrix $\Lambda$ that is similar to $A$. If $A$ has a full set of eigenvectors, then diagonalizing $A$ is easy and is given to us by eigen decomposition.



### Singular Value Decomposition

Once all the above things have been understood clearly, refer to [this note](https://ocw.mit.edu/courses/mathematics/18-06sc-linear-algebra-fall-2011/positive-definite-matrices-and-applications/singular-value-decomposition/MIT18_06SCF11_Ses3.5sum.pdf) for a preliminary explanation of SVD. Remember that in the note, the row space of an $m\times n$ matrix $A$ refers to all the vectors that can be mutliplied to $A$ (basically $\R^n$), and not the span of the rows of $A$ (denoted by $\bt{R}(A^T)$). We have already proved that $\bt{R}(A^T)  = \bt{N}(A)^\perp$. Thus, $\bt{R}(A^T)$ consists of all the vectors $\bt{x}$ such that $A\bt{x} \neq \bt{0}$.

Strang takes the identity $A = U\Sigma V^T$ as given, and shows us how to solve for $U$ and $V$. He doesn't exactly give us a proof of why every $m\times n$ matrix $A$ can be expressed as $U\Sigma V^T$. For a proof refer to [this link](https://gregorygundersen.com/blog/2018/12/20/svd-proof/#4-textbfu_i-is-a-unit-eigenvector-of-aatop).

Finally how do we solve $A=U\Sigma V^T$? 

$$
\begin{align}
A &= U\Sigma V^T \\
\implies A^TA &= (U\Sigma V^T)^T(U\Sigma V^T) \\
\implies A^TA &= (V\Sigma^T U^T)(U\Sigma V^T) \\
\implies A^TA &= V\Sigma^2 V^T \\
\end{align}
$$

Thus, we can get $\bt{v_i}$(s) from the eigen-decomposition of symmetric (semi-definite) matrix $A^TA$. We can also get $\sigma_i$(s) as the positive square-roots of the eigenvalues of $A^TA$. Finally, we can derive $\bt{u_i}$(s) from the formula

$$
AV = U\Sigma  \\
\textrm{OR} \\
A\bt{v_i} = \sigma_i \bt{u_i}\\
$$

This will give us only $r = \textrm{rank}(A)$ number of $\bt{u_i}$(s).  How do we find the $m-r$ remaining $\bt{u_i}$(s)? In that case we can just add the columns of $I_{m\times m}$ to the set of $\bt{u_i}$(s) that we found initially and then perform Gram-Schmidt algorithm on this set. 

Another way to go about it is to find the eigenvectors of $AA^T$, because

$$
AA^T = U\Sigma^2U^T
$$

However, in each given direction, there can be two different unit vectors $\bt{u_i}$ and $-\bt{u_i}$. Thus, we still need to ensure that each pair of $\bt{u_i}$ and $\bt{v_i}$ follow 

$$
A\bt{v_i} = \sigma_i \bt{u_i}\\
$$
