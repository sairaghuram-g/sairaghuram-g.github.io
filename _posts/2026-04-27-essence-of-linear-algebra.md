---
title: "Essence of Linear Algebra — My Notes from 3Blue1Brown"
date: 2026-04-27 00:00:00 +0530
categories: [Math, Linear Algebra]
tags: [linear-algebra, 3blue1brown, vectors, matrices, machine-learning]
math: true
---

These are my handwritten notes from 3Blue1Brown's *Essence of Linear Algebra* series, rewritten into a structured format. The series completely changed how I think about vectors, matrices, and transformations — not as symbol-pushing exercises, but as geometric intuition. These notes cover all 16 videos.

---

## Linear Algebra — What is a Vector?

A **vector** is the fundamental building block of linear algebra. But what *is* it? The answer depends on who you ask.

- **Physics**: A vector has a magnitude and a direction.
- **Computer Science**: A vector is an ordered list of numbers (a fancy list).
- **Math**: A vector can be anything that can be formed by addition and scalar multiplication.

The CS perspective is the most useful starting point. A vector like $\begin{bmatrix} 2 \\ 1 \end{bmatrix}$ tells us how to get to the tip of the vector from the origin of the coordinate system — move 2 units along x, then 1 unit along y.

In 3D, a vector $\begin{bmatrix} 2 \\ 1 \\ 3 \end{bmatrix}$ gives us three coordinates along the x, y, and z axes respectively.

---

### Vector Addition

$$\vec{v} + \vec{w} = \vec{r}$$

Geometrically, place the tail of $\vec{w}$ at the tip of $\vec{v}$. The resulting vector $\vec{r}$ goes from the tail of $\vec{v}$ to the tip of $\vec{w}$.

For example, if $\vec{v} = \begin{bmatrix} 1 \\ 2 \end{bmatrix}$ and $\vec{w} = \begin{bmatrix} 3 \\ -1 \end{bmatrix}$:

$$\begin{bmatrix} 1 \\ 2 \end{bmatrix} + \begin{bmatrix} 3 \\ -1 \end{bmatrix} = \begin{bmatrix} 1+3 \\ 2+(-1) \end{bmatrix} = \begin{bmatrix} 4 \\ 1 \end{bmatrix}$$

---

### Vector Multiplication (Scaling)

- Multiplying by a **positive number** stretches the vector in the same direction.
- Multiplying by a **negative number** flips the direction and scales the length.

---

### Basis Vectors and Span

$$\hat{i} = \text{unit vector along } x, \quad \hat{j} = \text{unit vector along } y$$

Any vector can be written as a linear combination of $\hat{i}$ and $\hat{j}$:

$$\begin{bmatrix} 3 \\ -2 \end{bmatrix} = 3\hat{i} + (-2)\hat{j}$$

The **span** of two vectors is the set of all linear combinations of those two vectors. Two vectors can span an entire 2D coordinate system — unless they are collinear (pointing in the same direction), in which case they only span a line.

If one vector in a set is redundant — meaning removing it doesn't change the span — it is called a **linearly dependent** vector. If every vector in the set adds a new direction to the span, they are **linearly independent**.

> **ML Connection**: In a dataset, you can think of each feature as a vector. Linearly dependent features don't contribute new information — they can be removed without loss, just like a redundant vector in a span.

---

## Linear Transformations (Video 3)

A **linear transformation** is a function that takes a vector as input and returns a transformed vector as output:

$$\vec{w} = f(\vec{v})$$

A transformation is **linear** if:
1. All lines remain lines (no curving).
2. The origin does not move.

The key insight: since every vector is expressed in terms of $\hat{i}$ and $\hat{j}$, once you know where $\hat{i}$ and $\hat{j}$ land after a transformation, you know where *every* vector lands. You only need to track the two basis vectors.

For example, if $\hat{i}$ lands on $\begin{bmatrix} 1 \\ 0 \end{bmatrix}$ and $\hat{j}$ lands on $\begin{bmatrix} -1 \\ 1 \end{bmatrix}$, the transformation matrix is:

$$\begin{bmatrix} 1 & -1 \\ 0 & 1 \end{bmatrix}$$

where the first column is where $\hat{i}$ lands and the second column is where $\hat{j}$ lands.

---

## Matrix Multiplication as Composition (Video 4)

If you need to apply two transformations one after another, instead of applying them sequentially, you can **multiply the transformation matrices** to get a single composite transformation.

Consider two transformations:
- $T_1$: Rotation by 90° — $\begin{bmatrix} 0 & -1 \\ 1 & 0 \end{bmatrix}$
- $T_2$: Shear — $\begin{bmatrix} 1 & 1 \\ 0 & 1 \end{bmatrix}$

Applying $T_1$ then $T_2$ gives the composite transformation $T_2 \cdot T_1$.

> **Critical**: When $T_1$ is applied first and then $T_2$, the notation is $T_2 \cdot T_1$ — **not** $T_1 \cdot T_2$. Order matters. Read right to left.

### How to Read a Matrix

$$T_1 = \begin{bmatrix} 1 & -2 \\ 1 & 0 \end{bmatrix}$$

- First column $\begin{bmatrix} 1 \\ 1 \end{bmatrix}$: where $\hat{i}$ lands.
- Second column $\begin{bmatrix} -2 \\ 0 \end{bmatrix}$: where $\hat{j}$ lands.

So when you apply $T_2$ on top of $T_1$:

$$\begin{bmatrix} 0 & 2 \\ 1 & 0 \end{bmatrix}\begin{bmatrix} -2 \\ 0 \end{bmatrix} = \begin{bmatrix} 0 \\ -2 \end{bmatrix}$$

### Why Matrix Multiplication Works the Way it Does

$$\begin{bmatrix} a_1 & b_1 \\ c_1 & d_1 \end{bmatrix} \begin{bmatrix} a_2 & b_2 \\ c_2 & d_2 \end{bmatrix} = \begin{bmatrix} a_1 a_2 + b_1 c_2 & a_1 b_2 + b_1 d_2 \\ c_1 a_2 + d_1 c_2 & c_1 b_2 + d_1 d_2 \end{bmatrix}$$

This formula isn't arbitrary — it's the direct result of tracking where $\hat{i}$ and $\hat{j}$ land after two successive transformations. That's also why **order is important**, and why matrix multiplication is **associative**:

$$A(BC) = (AB)C$$

because either way, $C$ is applied first, then $B$, then $A$.

---

## 3D Linear Transformations (Video 5)

In 3D, the same ideas apply. A transformation is represented by a 3×3 matrix where each column tells you where $\hat{i}$, $\hat{j}$, and $\hat{k}$ land respectively. While harder to visualize, the underlying logic is identical.

---

## Determinant (Video 6)

When any transformation is applied, the space between the basis vectors is **stretched or squished**. The **determinant** is the factor by which the area (or volume in 3D) between the basis vectors changes.

$$\det\begin{pmatrix} a & 0 \\ 0 & b \end{pmatrix} = a \cdot b$$

For a simple scaling matrix, the area scales by $a \times b$. For a general matrix, the determinant tells us the overall area scaling factor.

So what happens to $\hat{i}$ and $\hat{j}$ is also happening to the **entire matrix span**.

Key cases:
- **det = 3**: The area between the basis vectors is stretched to 3 times its original size.
- **det = 0**: All basis vectors become collinear — the transformation squishes space onto a line or a point. This is a critical signal.
- **det = −2**: The area is stretched by a factor of 2, but the **orientation of space is flipped** (like flipping a sheet of paper).

---

## Inverse Matrices (Video 7)

Matrices help us solve **systems of linear equations**. A system like:

$$2x + 5y + 3z = -3$$
$$4x + 8z = 0$$
$$x + 3y = 2$$

can be written in matrix form as:

$$A\vec{x} = \vec{v}$$

where $A$ is the coefficient matrix, $\vec{x}$ is the unknown vector, and $\vec{v}$ is the output vector.

Geometrically, $\vec{x}$ is the input vector that, when transformed by $A$, lands on $\vec{v}$.

### The Inverse

If we apply a reverse transformation $A^{-1}$ on $\vec{v}$, it should land back on $\vec{x}$:

$$A^{-1} A = I$$

where $I$ is the **identity matrix** — the transformation that does nothing:

$$I = \begin{bmatrix} 1 & 0 \\ 0 & 1 \end{bmatrix}$$

> $A^{-1}$ only exists if $\det(A) \neq 0$. If the determinant is zero, the transformation collapses space to a lower dimension, and there's no way to reverse it.

### Rank

- **Rank** = number of dimensions in the output of a transformation.
- For a 3×3 matrix, if rank is 2, the transformation squishes 3D space to a plane. If rank is 1, it squishes to a line.
- The set of all possible output vectors is called the **column space** of the matrix.
- The set of all vectors that land on the origin is called the **null space** (or **kernel**).

When the rank is reduced, many vectors collapse to the origin — meaning multiple input vectors map to the same output, so there are **multiple solutions** (or no unique solution).

---

## Non-Square Matrices as Transformations (Video 8)

A non-square matrix transforms space between different dimensions. For example, a 2×3 matrix transforms 3D space into 2D space. The 3 columns tell you where $\hat{i}$, $\hat{j}$, and $\hat{k}$ land in 2D.

$$\begin{pmatrix} 2 & 0 \\ -1 & 1 \\ -2 & 1 \end{pmatrix}$$

This takes a 3D vector and produces a 2D output.

---

## Dot Product and Duality (Video 9)

The **dot product** of two vectors:

$$\begin{bmatrix} 4 \\ 1 \end{bmatrix} \cdot \begin{bmatrix} 2 \\ -1 \end{bmatrix} = 4 \cdot 2 + 1 \cdot (-1) = 7$$

Geometrically, the dot product is: **project $\vec{w}$ onto $\vec{v}$, then multiply their lengths**.

- If the two vectors point in the **same direction**: dot product is **positive**.
- If they point in **opposite directions**: dot product is **negative**.
- If they are **perpendicular** ($\perp$): dot product is **0**.

### Why Does the Dot Product Represent Projection?

Consider a unit vector $\hat{a}$ with coordinates $(a_x, a_y)$.

When $\hat{a}$ is projected onto the x-axis, it lands at point $a_x$. When projected onto the y-axis, it lands at $a_y$. So $[a_x \; a_y]$ are the coordinates of $\hat{a}$.

Computing this projection transformation for any vector in space requires multiplying that vector with the row matrix $[a_x \; a_y]$ — which is exactly the dot product. That is the duality: a 1×n matrix (row vector) and a column vector are two perspectives on the same geometric operation.

**That's why the dot product is a projection.**

---

## Cross Product (Video 10)

Given two vectors $\hat{a}$ and $\vec{b}$ in 2D, the **cross product** is the **area of the parallelogram** formed by them.

$$\vec{v} \times \vec{w} = \det\begin{bmatrix} a & c \\ b & d \end{bmatrix}$$

The **orientation** (are $\vec{v}$ and $\vec{w}$ in counterclockwise order?) determines whether the cross product is positive or negative:

$$\hat{a} \times \hat{b} = -\hat{b} \times \hat{a}$$
$$\hat{i} \times \hat{j} = +1$$

In **3D**, the cross product $\vec{v} \times \vec{w}$ is not a scalar — it is a **vector**:
- Its **length** is the area of the parallelogram spanned by $\vec{v}$ and $\vec{w}$.
- Its **direction** is perpendicular to the plane of $\vec{v}$ and $\vec{w}$, determined by the **right-hand rule**: point your index finger along $\vec{v}$, your middle finger along $\vec{w}$, and your thumb points in the direction of $\vec{v} \times \vec{w}$.

$$\begin{bmatrix} v_1 \\ v_2 \\ v_3 \end{bmatrix} \times \begin{bmatrix} w_1 \\ w_2 \\ w_3 \end{bmatrix} = \det\begin{bmatrix} \hat{i} & v_1 & w_1 \\ \hat{j} & v_2 & w_2 \\ \hat{k} & v_3 & w_3 \end{bmatrix}$$

### Cross Product via Linear Transformations (Video 11)

To understand why this determinant formula gives the right answer, define a 3D-to-1D linear transformation in terms of $\vec{v}$ and $\vec{w}$. Find its dual vector $\vec{p}$ — the vector such that:

$$\vec{p} \cdot \begin{bmatrix} x \\ y \\ z \end{bmatrix} = \det\begin{bmatrix} x & v_1 & w_1 \\ y & v_2 & w_2 \\ z & v_3 & w_3 \end{bmatrix}$$

That dual vector $\vec{p}$ is exactly the cross product $\vec{v} \times \vec{w}$. The dot product with $\vec{p}$ represents projecting $\begin{bmatrix} x \\ y \\ z \end{bmatrix}$ onto $\vec{p}$ and multiplying by its length — giving the volume of the parallelepiped.

---

## Cramer's Rule (Video 12)

Cramer's Rule gives a geometric method to solve $A\vec{x} = \vec{v}$.

Consider:
$$3x + 2y = -4$$
$$-x + 2y = -2$$

In matrix form: $\begin{bmatrix} 3 & 2 \\ -1 & 2 \end{bmatrix}\begin{bmatrix} x \\ y \end{bmatrix} = \begin{bmatrix} -4 \\ -2 \end{bmatrix}$, with $\det(A) \neq 0$.

After transformation $A$: $x$ basis vector lands on $\begin{bmatrix} 3 \\ -1 \end{bmatrix}$ and $y$ basis vector lands on $\begin{bmatrix} 2 \\ 2 \end{bmatrix}$.

The area before transformation = $\det\begin{bmatrix} 2 & -1 \\ 0 & 1 \end{bmatrix}$

The area after transformation = $\det\begin{bmatrix} 2 & 4 \\ 0 & 2 \end{bmatrix}$

So:
$$y = \frac{\det\begin{bmatrix} 2 & 4 \\ 0 & 2 \end{bmatrix}}{\det\begin{bmatrix} 2 & -1 \\ 0 & 1 \end{bmatrix}}$$

Similarly for $x$. Cramer's Rule is geometrically elegant — each unknown is the ratio of a determinant of a modified matrix to the determinant of $A$.

---

## Change of Basis (Video 13)

The way we represent vectors can change with a change in basis. When we describe a vector using different basis vectors, the coordinates change — but the underlying geometric object does not. Change of basis is the mathematical machinery for switching between different coordinate systems.

---

## Eigenvalues and Eigenvectors (Video 14)

Consider the transformation $\begin{bmatrix} 3 & 1 \\ 0 & 2 \end{bmatrix}$. Most vectors get knocked off their original span after transformation. However, some special vectors **remain on their own span** — they only get scaled, not rotated.

For example, $\hat{i} = \begin{bmatrix} 1 \\ 0 \end{bmatrix}$ lands on $\begin{bmatrix} 3 \\ 0 \end{bmatrix}$ — still on the x-axis, just scaled by 3.

These special vectors are called **eigenvectors** of the transformation. Each eigenvector has an associated **eigenvalue** — the factor by which it is stretched or squished.

$$A\vec{v} = \lambda\vec{v}$$

where $A$ is the transformation matrix, $\vec{v}$ is an eigenvector, and $\lambda$ is the eigenvalue.

Eigenvalues can be **negative** (vector flips direction) or even **complex** (meaning no real eigenvector exists — like in a pure rotation).

### Geometric Intuition

Since an eigenvector stays in its own span through the transformation, in 3D, an eigenvector with eigenvalue 1 represents the **axis of rotation** of the transformation.

### How to Find Eigenvalues

Rewrite $A\vec{v} = \lambda\vec{v}$ as:

$$(A - \lambda I)\vec{v} = \vec{0}$$

We need a non-zero $\vec{v}$, so $(A - \lambda I)$ must squish space to zero — which means:

$$\det(A - \lambda I) = 0$$

Solve this for $\lambda$. If this yields complex roots (like $\lambda^2 + 1 = 0 \Rightarrow \lambda = \pm i$), there are **no real eigenvectors**.

### The λI Trick

To make sense of $\lambda\vec{v}$ as a matrix operation, write $\lambda$ as:

$$\lambda I = \begin{bmatrix} \lambda & 0 & 0 \\ 0 & \lambda & 0 \\ 0 & 0 & \lambda \end{bmatrix}$$

Then $(A - \lambda I)\vec{v} = \vec{0}$ is a proper matrix equation.

### Eigen Basis

If the basis vectors are changed to eigenvectors, the resulting matrix is **diagonal** — each diagonal entry is the corresponding eigenvalue. This simplifies many computations enormously.

---

## Quick Tips for Computing Eigenvalues (Video 15)

Two powerful properties:

- **Trace** of a matrix = sum of diagonal entries = sum of eigenvalues (the mean, basically).
- **Determinant** of a matrix = product of eigenvalues.

So if a 2×2 matrix has mean eigenvalue $m$ and product of eigenvalues $p$:

$$\lambda_1, \lambda_2 = m \pm \sqrt{m^2 - p}$$

This is a fast mental shortcut without expanding the full characteristic polynomial. It makes more geometric sense than algebraic sense — think about it!

---

## Abstract Vector Spaces (Video 16)

We understood that transformations apply to vectors, and that the *way* we represent vectors can change with basis. But here's the deep insight: **determinants, eigenvalues, and eigenvectors are independent of the coordinate system.** They are intrinsic properties of the transformation.

This opens a broader perspective: **functions also exhibit vector-like properties**.

- $f(x) + g(x)$ is analogous to vector addition.
- A linear transformation where input is $f(x)$ and output is $g(x)$ is analogous to matrix multiplication.
- A good example: **derivatives and integrals** are linear transformations on the space of functions.

The entire framework of linear algebra — span, basis, linear independence, linear transformations, eigenvectors — generalizes far beyond arrows in space. Any mathematical object that supports addition and scalar multiplication, and where linearity holds, can be treated as a "vector." This is the abstract vector space perspective, and it's the foundation for understanding why techniques from linear algebra appear everywhere in physics, engineering, and machine learning.

---

## Summary

| Concept | Geometric Meaning |
|---|---|
| Vector | Arrow from origin; list of coordinates |
| Span | All reachable points via linear combinations |
| Linear Transformation | Function that keeps lines as lines and origin fixed |
| Matrix | Encoding of where $\hat{i}$ and $\hat{j}$ land |
| Matrix Multiplication | Composition of two transformations |
| Determinant | Area/volume scaling factor of the transformation |
| Inverse | Reverse transformation; exists only if det ≠ 0 |
| Rank | Dimension of the output space |
| Null Space / Kernel | Vectors that collapse to origin |
| Dot Product | Projection of one vector onto another × lengths |
| Cross Product | Area of parallelogram; perpendicular vector (3D) |
| Eigenvalue | Scaling factor during transformation for eigenvectors |
| Eigenvector | Vector that stays on its own span during transformation |
| Trace | Sum of diagonal entries = sum of eigenvalues |

---

*Notes based on [3Blue1Brown's Essence of Linear Algebra](https://www.youtube.com/playlist?list=PLZHQObOWTQDPD3MizzM2xVFitgF8hE_ab) — one of the best mathematical series on the internet. Highly recommended to watch alongside these notes.*
