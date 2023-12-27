---
layout: default
title: EigenDecomposition
slug: eigen
item_num: 5
excerpt: In the last note, we looked at our first application of Linear Algebra in Machine Learning. Here we look at EigenDecomposition, which again has lots of ML applications, one of the most common being PCA. We will also discuss Symmetric Matrices and Quadratic Functions (which are widely used in Probability and Optimization).
---

$$
\newcommand{\mat}[1]{\begin{bmatrix} #1 \end{bmatrix}}
\newcommand{\bt}[1]{\mathbf{#1}}
$$



# EigenDecomposition

*In the last note, we looked at our first application of Linear Algebra in Machine Learning. Here we look at EigenDecomposition, which again has lots of ML applications, one of the most common being PCA. We will also discuss Symmetric Matrices and Quadratic Functions (which are widely used in Probability and Optimization).*



### Change of Basis


Let $\bt{a_1}, \dots, \bt{a_n}$ be a basis for the vector space $\mathcal{V}$ over the field $\mathbb{F}$. 

Define the function $f: \mathbb{F^n} \to \mathcal{V}$, as

$$
f([x_1, \dots, x_n]) = x_1\bt{a_1} + \dots + x_n\bt{a_n} \\
$$

That is, $f$ maps the representation of a vector in $\bt{a_1}, \dots, \bt{a_n}$ to the vector itself. The coordinate representation is also a vector in itself. The Unique Representation Lemma tells us that every vector in $\mathcal{V}$ has exactly one representation in terms of the basis vector, so the functions $f$ is both onto and one-to-one, hence it is invertible.  

The inverse function $f^{-1}$ takes a vector $\bt{v}$ in $\mathcal{V}$ and maps it to a vector of coordinates $[x_1, \dots, x_n]$ such that

$$
\mat{ \, & \, & \, \\ \, & \, & \, \\ \bt{a_1} & \dots & \bt{a_n} \\ \, & \, & \, \\ \, & \, & \,} \mat{x_1 \\ \vdots \\ x_n} = \bt{v}
$$


The inverse of a linear function is also linear and hence $f^{-1}$ can be represented by a matrix $C$, known as the change of basis matrix.


Now watch 3Blue1Brown's video on [how to represent a linear transformation in a new basis set](https://youtu.be/P2LTAUO1TdA?t=537). This concept is quintessential for a good understanding of Eigendecomposition and SVD.


### Eigenvectors and Eigenvalues

There might be some vectors during a linear transformation, that only get stretched or squished (and don't change their direction). Scalar multiples of such vectors will also have the same property of not changing their direction. Such vectors are called the eigenvectors of a transformation. The factor by which an eigenvector is stretched or squished is called the eigenvalue of that eigenvector.  

It should be obvious that eigenvectors exist only for square matrices. They can be singular or invertible, symmetric or triangular or diagonal; but eigendecomposition can be performed only on square matrices.

If $\bt{v}$ is the eigenvector for a transformation $A$, and the corresponding eigenvalue is $\lambda$, then  

$$A\bt{v} = \lambda\bt{v}$$  

$$\implies(A - I\lambda)\bt{v} = \bt{0}$$  

If $\textrm{det}(A - \lambda I) \neq 0$, then $\bt{v} = \bt{0}$ is the only solution of the above equation. Therefore eigenvectors exist only if $\textrm{det}(A - \lambda I) = 0$.  

Thus, the method of finding eigenvectors is as follows:
* Find $\lambda$ by solving the equation $\textrm{det}(A - \lambda I) = 0$.
* Sequentially plug in each value of $\lambda$ and derive the matrix $(A - I\lambda)$.
* Solve $(A - I\lambda)\bt{v} = \bt{0}$ to find $\bt{v}.$

Suppose $P$ is the matrix of a projection onto a plane. For any $\bt{x}$ in the plane $P\bt{x} = \bt{x}$, so $\bt{x}$ is an eigenvector with eigenvalue $1$. A vector $\bt{x}$ perpendicular to the plane has $P\bt{x} = \bt{0}$, so this is an eigenvector with eigenvalue $\lambda = 0$. The eigenvectors of $P$ span the whole space (but this is not true for every matrix).

### Finding Eigenvalues

We know that in order to find the eigenvalues of a matrix $A$, we need to solve:

$$
\|A - \lambda I\| = 0
$$

The determinant of a matrix is computed by solving the characteristic polynomial. The characteristic polynomial of a 2×2 matrix is a $2^\text{nd}$ degree algebraic equation, meaning there are two $\lambda$s that satisfy the equation (they might be complex). The solutions can be found using the quadratic formula:

$$
 \lambda = \frac{-b \pm \sqrt{b^2 - 4ac}}{2a} \tag{1} \label{eq:quadratic}
$$

The Fundamental Theorem of Algebra states that any $m$-degree polynomial has $m$ solutions. And because an $m \times m$ matrix has an $m$-th order characteristic polynomial, it will have $m$ roots, or $m$ eigenvalues. Hence, an $m \times m$ matrix has $m$ eigenvalues (some of those eigenvalues may be repeated, complex numbers, or zeros).

### Diagonalization via EigenDecomposition  

Let us say that an $m \times m$ matrix contains $m$ eigenvalues and $m$ associated eigenvectors. The set of eigenvalue/vector pairs produces a set of similar-looking equations:

$$
A\bt{v_1} = \lambda \bt{v_1}  \\
A\bt{v_2} = \lambda \bt{v_2}  \\
\vdots
$$

All of these equations can be simplified by having each eigenvector be a column in a matrix, and having each eigenvalue be an element in a diagonal matrix.

$$
A V = V \Lambda
$$

Now, if the $m$ eigenvectors are independent, they form a basis for the input space and $V$ can be inverted. As a result, 

$$
A = V \Lambda V^{-1}
$$

Thus, matrix $A$ is diagonal in basis $V$. That’s why eigendecomposition is also sometimes called *diagonalization*. To diagonalize a matrix $A$ means to find some matrix of basis vectors such that $A$ is a diagonal matrix in that basis space. Watch 3Blue1Brown's video on [eigenvectors and eigenvalues](https://www.youtube.com/watch?v=PFDu9oVAE-g) for an in-depth explanation.

Remember that we needed our eigenvectors to be linearly independent to form a basis set. When is this assumption valid? We discuss this below.

### Conditions for Diagonalization  

Many square matrices have all distinct eigenvalues. That’s nice because distinct eigenvalues always lead to distinct eigenvectors. The intuition is easy to catch. Distinct eigenvalues suggest that the corresponding eigenvectors are being squished / stretched by different amounts, and hence can't be pointing in the same direction (matrix multiplication is linear). A more rigorous proof is given in Section 15.6 of the Linear Algebra book by Mike X Cohen. 

Notice that we did not need to impose any assumptions about the field from which the $\lambda$s are drawn; they can be real or complex-valued, rational or irrational, integers or fractions. The only important quality is that each $\lambda$ is distinct.  

Repeated eigenvalues complicate matters because they sometimes have distinct eigenvectors and sometimes not. For example, $$\mat{4 & 0 \\ 0 & 4}$$ has $4$ as the repeated eigenvalue but two distinct eigenvectors $$\mat{1 \\ 0}$$ and $$\mat{0 \\ 1}$$. Remember, we call two eigenvalues distinct when $\lambda_1 \neq \lambda_2$ but we call two eigenvectors distinct when they are linearly independent. 

Surprisingly, even the zero matrix has two repeated eigenvalues of $0$, but two distinct eigenvectors. Notice that zero is an acceptable eigenvalue but zero vector cannot be called an eigenvector. Non-trivial vectors in the null space of $A$ are eigenvectors of $A$.  

Repeated eigenvalues can lead to one of two situations. First, both eigenvectors can lie on the same 1D subspace. In that case, the eigenspace won’t span the entire input space $\mathbb{R}^M$; it will be a smaller-dimensional subspace. The second possibility is that there are two distinct eigenvectors associated with one eigenvalue. In this case, there isn’t a unique eigenvector; instead, there is a unique eigenplane and the two eigenvectors are basis vectors for that eigenplane. Any two independent vectors in the plane can be used as a basis.  

### Complex Eigenvalues  

If $4ac \gt b^2$ in equation $\eqref{eq:quadratic}$, then you end up with the square root of a negative number, which means the eigenvalues will be complex numbers. And complex eigenvalues lead to complex eigenvectors.  

For a $2 \times 2$ matrix, complex conjugate pair solutions are immediately obvious from Equation $\eqref{eq:quadratic}$: A complex number can only come from the square-root in the numerator, which is preceded by a $\pm$ sign. Thus, the two solutions will have the same real part and flipped-sign imaginary part. This generalizes to larger matrices: A real-valued matrix with complex eigenvalues has solutions that come in pairs: $\lambda$ and $\bar{\lambda}$. Furthermore, their associated eigenvectors also come in conjugate pairs $\bt{v}$ and $\bt{\bar{v}}$.

$$
\begin{align}
A\bt{v} &= \lambda\bt{v} \\
\overline{A\bt{v}} &= \overline{\lambda\bt{v}} \\ 
A\bt{\bar{v}} &= \bar{\lambda} \bt{\bar{v}} \\
\end{align}
$$

Last equation follows because $A$ has real-valued enteries. Also, if $a$ and $b$ are complex numbers, then $\overline{ab} = \bar{a} \bar{b}$.   

It is obvious that if $\lambda$ has a complex part, then the corresponding eigenvector also should have a complex part (distinct eigenvavlues lead to distinct eigenvectors). We can also prove that if the eigenvalue is real, then there exists a real-valued eigenvector corresponding to the real eigenvalue. [Proof](https://sharmaeklavya2.github.io/theoremdep/nodes/linear-algebra/eigenvectors/real-matrix-with-real-eigenvalue-has-real-eigenvectors.html).

### Powers of a Matrix  

We use $A^2$ to denote application of $A$ transform twice. In general, it is a very difficult task to compute $A^k$ (for large $k$) even for small matrices. Eigenvalue Decomposition gives us a very easy way of doing the same. If we can write $A$ as $V\Sigma V^{-1}$, then  

$$
A^k = (V\Sigma V^{-1}) (V\Sigma V^{-1}) \dots(V\Sigma V^{-1}) = V\Sigma^kV^{-1}
$$

This equation makes intuitive sense. Once you shift a vector from normal basis to eigenbasis, repeated application of the transform just scales each component (along each eigenvector) repeatedly by the corresponding eigenvalue.  

EigenDecomposition is also helpful to find the inverse of a matrix. It is easy to see that the inverse of a diagonal matrix is the diagonal matrix with elements individually inverted. That’s the key insight to inverse-via-eigendecomposition.

$$
A^{-1} = (VDV^{-1})^{-1} = VD^{-1}V^{-1} \\
$$


### Symmetric Matrices

If $S$ is a symmetric matrix, then $S = S^T$. Notice that symmetric matrices are not always invertible (they don't have trivial null spaces). For example ${\bt{0}_{n\times n}}$ is symmetric but not invertible. Identity matrix with some diagonal entries changed to zero is also symmetric but not invertible.   

**Property 1: Real Eigenvalues**  Suppose $S$ is a $m\times m$ symmetric matrix with real valued enteries (always assume enteries are real, unless otherwise mentioned). Let's prove that all of its $m$ eigenvalues are real-valued. 

Let the superscript ${}^H$ denote the Hermitian transpose, which means transponse and flip the sign of the imaginary parts.

$$
\begin{align}
& S\bt{v} = \lambda  \bt{v}  \\
\implies &(S\bt{v})^H = (\lambda  \bt{v})^H  \\
\implies &\bt{v}^H S = \lambda^H \bt{v}^H  \\
\implies &\bt{v}^H S \bt{v} = \lambda^H \bt{v}^H \bt{v} \\
\implies &\lambda \bt{v}^H \bt{v} = \lambda^H \bt{v}^H \bt{v} \\ 
\implies &\lambda = \lambda^H \\
\end{align}
$$

$\bt{v}^H \bt{v}$ is the magnitude squared of vector $\bt{v}$ and can simply be divided away (remember that $\bt{v} \neq \bt{0}$).

$$
\bt{v}^H \bt{v} = \mat{\bar{v_1} &  \bar{v_2} & \dots & \bar{v_n}} \mat{v_1 \\ v_2 \\ \vdots \\ {v_n}} = \|v_1\|^2 + \|v_2\|^2 + \dots +  \|v_n\|^2 
$$

A number is equal to its complex conjugate only when its imaginary part is equal to zero, i.e., it is a real-valued number. This concludes the proof that eigenvalues must have an imaginary part equal to 0, which means it is real-valued.

**Property 2: Orthogonal Eigenvectors** If the matrix is symmetric, then all of its eigenvectors are pairwise orthogonal. Let us prove that the dot product between any pair of eigenvectors is zero. We assume that $\lambda_1$ and $\lambda_2$ are two distinct eigenvalues of $S$. 

$$
\lambda_1\bt{v_1}^T \bt{v_2} = (S\bt{v_1})^T \bt{v_2} =  \bt{v_1}^T S^T \bt{v_2} = \bt{v_1}^T S \bt{v_2} = \lambda_2\bt{v_1}^T \bt{v_2}
$$

Thus,

$$
(\lambda_1 - \lambda_2) \bt{v_1}^T \bt{v_2} = 0
$$

If the two eigenvalues are distinct, then the dot product is zero. If they are not distinct, then we can choose two orthogonal eigenvectors from the eigenplane. Notice that $S$ doesn't exactly have to be invertible. If a vector $\bt{x}$ belongs to the null space of $S$, it is still an eigenvector with $\lambda = 0$.

Thus, if $S_{n\times n}$ is a symmetric matrix, then it is possible to choose a set of $n$ eigenvectors that are orthogonal to each other. Let $Q$ be the matrix whose columns are the orthonormal eigenvectors of $S$. Then

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
(rank one) matrices! This is known as the Spectral Theorem.  

### Quadratic Form and Definiteness 

If $A$ is a square matrix of size $m \times m$, and $\bt{x}$ is a vector of size $m$, then notice that $\bt{x}^T A \bt{x}$ is a scalar value, representing a quadratic function of the enteries in $\bt{x}$. 

$$\bt{x}^T A \bt{x}$$ 

is called the Quadratic Form of matrix $A$.  

Any quadratic function $f(x_1, \dots, x_n)$ can be written in the form of $\bt{x}^T Q \bt{x}$, where $Q$ is a symmetric matrix and $q_{ij}$ is half of the coefficient of $x_ix_j$ term in $f$.  

Also, any quadratic form $\bt{x}^T A \bt{x}$ (where $A$ is not a symmetric matrix), can be written as $\bt{x}^T Q \bt{x}$, where $Q$ is a symmetric matrix and $q_{ij} = \frac{1}{2}(a_{ij} + a_{ji})$. See [these slides](https://laurentlessard.com/teaching/cs524/slides/11%20-%20quadratic%20forms%20and%20ellipsoids.pdf) for more details.  


**Positive Definite Matrix** A positive definite matrix is a *symmetric matrix* for which all eigenvalues are positive.

For a positive definite matrix $A$,

$$
\begin{align}
\bt{x}^TA\bt{x} &> 0 &(\forall \bt{x}, \bt{x}\neq \bt{0})
\end{align}
$$  

This is easy to prove intuitively when you think of $A$ in terms of its Spectral Decomposition. $A\bt{x}$ gives us a vector whose projections on the orthogonal vectors $\bt{q_i}$ are linearly scaled in the same direction (positive eigenvalues). Therefore, when you take the dot product of $A\bt{x}$ and $\bt{x}$, all the elements along the various $\bt{q_i}$(s) will have a non-negative product and $\bt{x}^TA\bt{x} > 0$.  

Let $S = A^T A$. Then,

$$
\begin{align}
\bt{x}^T S \bt{x} &= \bt{x}^T A^T A \bt{x} \\
&= (A\bt{x})^T A \bt{x} \\
&= \|A\bt{x}\|^2
\end{align}
$$ 

 Magnitudes cannot be negative. A magnitude (and thus, the quadratic form) can be zero when $A$ has non-trivial null-space. In any case, $S$ is atleast positive semi-definite.  

 Remember that all matrices of the form $S = A^T A$ are symmetric, but not all symmetric matrices can be expressed as $A^T A$. Only positive (semi)definite matrices can be expressed as $A^T A$, and $A$ is called the square-root of $S$. See [these slides](https://laurentlessard.com/teaching/cs524/slides/11%20-%20quadratic%20forms%20and%20ellipsoids.pdf) for more details.  

**Ellipse and Ellipsoid** Remember that an ellipse in 2D is given by

$$
\frac{x^2}{a^2} + \frac{y^2}{b^2} = 1
$$

If $a > b$, then $a$ is called the semi-major axis. If $a < b$, then $b$ is the semi-major axis. If $a=b$, then the points form a circle with radius $a$. The equation for an ellipsoid in $n$ dimensions is:

$$
\frac{x_1^2}{a_1^2} + \frac{x_2^2}{a_2^2} + \cdots + \frac{x_n^2}{a_n^2} = 1
$$

The equations above represent ellipsoids whose axes coincide with the axes of the coordinate system. These equations can be represented in matrix lingo as $\bt{x}^T\Lambda\bt{x}$, where $\Lambda$ is a diagonal matrix. What if the axes of the ellipsoid don't fall on the axes of the coordinate system? Then the ellipsoid will be of the form $\bt{x}^TA\bt{x}$, where $A$ is positive definite. We know that $A=Q\Lambda Q^T$, where $Q$ is orthonormal and $Q^T = Q^{-1}$. If we perform change of basis to $Q$, then the equation again becomes $\bt{z}^T\Lambda \bt{z}$, where $\bt{z}$ are the coordinates in the eigen-basis. Thus, $\bt{x}^TA\bt{x}$ represents an ellipsoid whose axes are along the eigenvectors of $A$.

### Additional Resources

1. [3B1B's video](https://youtu.be/e50Bj7jn9IQ) on the relationship between eigenvalues and trace of a matrix
2. [Covariance Matrix Note](https://cds.nyu.edu/wp-content/uploads/2021/05/covariance_matrix.pdf) from NYU Course on [Math Tools](https://cds.nyu.edu/math-tools/) 
3. Lec 6 (second half) of ECE-532 on Positive Definite Matrices and 3D ellipses


