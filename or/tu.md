TU is a property by which a linear program will always have an integral solution.
All you need to prove is that in your LP
 - A: matrix is TU
 - b: column has only integers

## What is a a Total Unimodularity (TU) Matrix

A matrix A is Totally Unimodular (TU) if each square submatrix S of A has det(S)=0,1 or −1.

### Properties

The following are equivalent:
1. A is TU.
2. The transpose of A is TU.
3. (A, I) is TU.
4. A matrix obtained by deleting a unit row/column from A is TU.
5. A matrix obtained by multiplying a row/column of A by -1 is TU.
6. A matrix obtained by interchanging two rows/columns of A is TU.
7. A matrix obtained by duplicating rows/columns of A is TU.
8. A matrix obtained by a pivot operation on A is TU.
• We can easily show that if A is TU, it remains so after adding slack
variables, adding simple bounds on the variables, or adding ranges on the
constraints (how?).
• We can also show that the polyhedron corresponding to the dual LP is
integral

### Recognizing Totally Unimodular Matrices

A is TU if and only if for every J ⊆ {1, . . . , n}, there exists a partition J1, J2 of J such that:

$$|\sum_{j \in J_1} a_{ij} - \sum_{j \in J_1} a_{ij}| \leq 1 \forall i = 1, \dots, m$$

Corollary 1. If the (0, 1, -1) matrix A has no more than two nonzero 
entries in each column, and if $\sum_i a_{ij} = 0$ if column j contains two
nonzero coefficients, then A is TU.

## Proofs

### The adjugate matrix of an TU matrix is integral

The formula for the adjugate matrix is given by:

$$adj(A)=C^T$$

We have:

$$A \times adj(A)=det(A) I$$

$C_{ij} = (-1)^{n+m} M_{n,m}$ with $M_{n,m}$, the determinant of the matrix A 
with the row n and column m removed.

To show that the adjugate matrix is integral, we need to demonstrate that 
each element of $C_{ij}$ is an integer.

#### Base Case (n = 1):

The determinant of the 0×0 matrix is 1 
Since the minor $M_{11}$ of a 1×1 matrix is the determinant of a 0×0 matrix, 
and that determinant is 1, therefore $M_{11}=1$.

Therefore, the cofactor matrix of a 1×1 matrix is the a 1×1 identity matrix I=[1], which is integral.

#### General Case

Consider the n x n totally unimodular matrix A.

Removing one row and column gives a TU matrix. So any minor of A is also a TU (n-1) x (n-1) matrix.

The cofactor $C_{ij}$ for each element a_ij is given by $C_{ij} = (-1)^{n+m} M_{n,m}$ with $M_{n,m}$,
the determinant of the matrix A without the row n and column m.
The determinant of the minor $M_{n,m}$ is equal to the determinant of a TU matrix 
that is equal to 0, 1 or −1.

Therefore, each $C_{ij}$ is an integer.
Hence, the adjugate matrix of a totally unimodular matrix is integral.

### A TU Matrix guarantees integral solution for a LP

A TU matrix with slack variable is still a TU Matrix (We add an identity matrix to it).

Consider the LP problem $Ax=b$  with basis B, 
the value of basic variables $x_B$ can be obtained as:

$$x_B=B^{−1}b=\frac {adj(B)}{det(B)}b$$

 - B is TU $\Rightarrow$ det(B)=−1 or 1
 - [The adjugate matrix of a TU matrix is also integral](#The-adjugate-matrix-of-an-TU-matrix-is-integral) it implies that $B^{−1}$ is integral

Since b is integral, then $x_B$ is also integral, 
hence guaranteeing and integral optimum for the LP.

# References

  - [1]: https://or.stackexchange.com/questions/4471/what-is-a-general-procedure-to-prove-that-the-lp-relaxation-of-an-ip-delivers-th
  - [2]: https://en.wikipedia.org/wiki/Minor_(linear_algebra)#First_minors