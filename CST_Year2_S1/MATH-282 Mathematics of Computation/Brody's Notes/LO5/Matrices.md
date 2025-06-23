```
\begin{bmatrix}\end{bmatrix}
```

$$ \begin{bmatrix}3 & -6\\0 & 1\\49.5 & -2.5\end{bmatrix} $$
Matrices are often indicated using capital letters such as A, B.
Entries in matrices can be referenced using lowercase letters such as $a_{3,2}$ (entry in row 3, column 2)
# Matrix Math
## Addition
To add two matrices, add corresponding elements of the two operands.
Restrictions: operands must be of the same size.

Example
$$\begin{bmatrix}3 & -6\\0 & 1\\49.5 & -2.5\end{bmatrix} + \begin{bmatrix}4 & 2.5\\-1 & 0\\1 & 6\end{bmatrix} = \begin{bmatrix}3 + 4 & -6 + 2.5\\0 + -1 & 1 + 0\\49.5 + 1 & -2.5 + 6\end{bmatrix} = \begin{bmatrix} 7 & -3.5\\-1 & 1\\50.5 & 3.5\end{bmatrix}$$
Note that the resultant sum matrix will be the same size as the operands.

Also note that the order of operands does not matter: A + B = B + A
## Subtraction
To subtract two matrices, subtract corresponding elements of the two operands.
Restriction: operands must be of the same size.

Example:
$$\begin{bmatrix}3 & -6\\0 & 1\\49.5 & -2.5\end{bmatrix} - \begin{bmatrix}4 & 2.5\\-1 & 0\\1 & 6\end{bmatrix} = \begin{bmatrix}3 - 4 & -6 - 2.5\\0 - -1 & 1 - 0\\49.5 - 1 & -2.5 - 6\end{bmatrix} = \begin{bmatrix} -1 & -8.5\\1 & 1\\48.5 & -8.5\end{bmatrix}$$
Note that resultant difference matrix will be the same size as the operands.

Order of operands *does* matter because A - B != B - A. For instance, if we call the matrices above A and B, then B - A is:
$$\begin{bmatrix}4 & 2.5\\-1 & 0\\1 & 6\end{bmatrix} - \begin{bmatrix}3 & -6\\0 & 1\\49.5 & -2.5\end{bmatrix} = \begin{bmatrix}3 - 4 & -6 - 2.5\\0 - -1 & 1 - 0\\49.5 - 1 & -2.5 - 6\end{bmatrix} = \begin{bmatrix} -1 & -8.5\\1 & 1\\48.5 & -8.5\end{bmatrix}$$
![[Pasted image 20241011082535.png]]
## Scalar multiplication
Scalar multiplication is multiplying a matrix by a scalar (sing dimensionless) value. We multiple each element by the scalar value.

Restrictions: none
$$\begin{bmatrix} 4 & -1 \\ 05 & 0 \end{bmatrix} * 10 = \begin{bmatrix}\end{bmatrix}$$
Resultant product matrix is the same size as the original matrix.

Order of operation does not matter, so $q * A = A * q$.
>Note that $A - B = -1 * (B - A)$, and similarly, $B - A = -1 * (A - B)$
## Matrix multiplication
In matrix multiplication, we identify the row in the left operand and the column in the right operand and use them. Take corresponding elements in that row and that column and multiple them, and then add up those products to get the value in the resultant matrix.

Example: For a 2x2 matrix multiplied by a 2x2 matrix, we get a 2x2 product matrix. We will look at rectangular matrices later.
$$\begin{bmatrix}5 & -1 \\ 3 & 0\end{bmatrix} * \begin{bmatrix}2 & 4 \\ -6 & 8\end{bmatrix} = \begin{bmatrix}5 * 2 + -1 * -6 & 5 * 4 + -1 * 8 \\ 3 * 2 + 0 * -6 & 3 * 4 + 0 * 8\end{bmatrix} = \begin{bmatrix}16 & 12 \\ 6 & 12\end{bmatrix}$$
If we call the two matrices A and B, then we can also calculate B \* A:
$$\begin{bmatrix}2 & 4 \\ -6 & 8\end{bmatrix} * \begin{bmatrix}5 & -1 \\ 3 & 0\end{bmatrix} = \begin{bmatrix}2 * 5 + 4 * 3 & 2 * -1 + 4 * 0 \\ -6 * 5 + 8 * 3 & -6 * -1 + 8 * 0\end{bmatrix} = \begin{bmatrix}22 & -2 \\ -6 & 6\end{bmatrix}$$
Note that A \* B != B \* A, so matrix multiplication is *not* commutative (order of operands is important).

Example: Using visual matrix multiplication method - put the second operand above and to the right of the first operand in a triangle, calculating the result where the rows and column intersect.

$$\begin{bmatrix}-2 & 3 \\ 0 & -5\end{bmatrix}$$
$$\begin{bmatrix} 1 & 3 \\ -1 & 0\end{bmatrix} \begin{bmatrix}-2 & -12 \\ 2 & -3\end{bmatrix} = \begin{bmatrix}1 * -2 + 3 * 0 & 1 * 3 + 3 * -5 \\ -1 * -2 + 0 * 0 & -1 * 3 + 0 * -5\end{bmatrix}$$
>See the student notes for more practice.
### Excel MMULT
![[Pasted image 20241011091722.png]]
## Generalization
For matrices of size $m_1 * n_1$ and $m_2 * n_2$, the two matrices can only be multiplied if $n_1 = m_2$ (inner dimensions must be equal) and the product matric will be of size ?.
## Matric Division
To do division, we must find the inverse matric (if possible) and multiply by it. We will not look at this for now. Be aware that just like solving 2x = 7 involves multiplying both sides by the inverse of 2 (which is 1/2), we can multiply matrices by inverse matrices.
# Coding Matric Classes

- Created `IMartix` interface in java, see `MATH282\LO3_5\`
- Abstract class about implementation details
	- Getters and setters
	- Creating new matrix
		- Children will implement this
- Concreate child class implements matrix
	- 2D array of doubles for the values
## Todo
- [ ] Implement scalarMultiply
- [ ] Implement subtract
- [ ] Implement matrix multiple
- [x] Update the matrix constructor to make a deep copy of array
- [x] Create copy matrix method
- [x] Create zero filled matrix (takes in rows and cols)
---
# Using matrices to represent graphic object
### 2-dementional object
Can be represented as a set of data points, which can be stored in an N\*2 matrix (for now), where N is the number of data points.

Three transformations we can do to graphic objects are:
1. Scaling: making the object bigger or smaller
2. Translation: move the object
3. Rotation: rotate the object around some point
#### Scaling
To scale the object by some factors $S_x$ and $S_y$:
x' (Prime) = x \* $S_x$
y' = y \* $S_y$
>This will also move the object away its origin
#### Translation
To translate the object by some amount $T_x$ and $T_y$:
x' = x + $T_x$
y' = y + $T_y$
#### Rotation
To rotate clockwise by some angle $\theta$ (in radians - recall that radians = degree \* $\pi$/180)
x' = x \* cos $\theta$ + y \* sin $\theta$
y = -x \* sin $\theta$ + y \* cos $\theta$
>This will also move the object away its origin
##### Dealing with side effects
We saw that scaling and rotation also moved the object. Rotation or scaling is done around the "world origin" (0, 0). We need to pick a "local origin'" to rotate or scale about its own origin. To do so:
1. *Translate* the object to the world origin
2. Scale or rotate the object
3. *Translate* back to the local origin

Basically: Move to (0, 0), do change, move back to original place.