*The determinant definition can stem from desired properties or*
*the properties can stem from the definition. we will take the approach of*
*showing the properties stem from the definition.*

### Resources
- [statlect](https://www.statlect.com/matrix-algebra/determinant-of-a-matrix)
- 
### Definition
$$det(A) = \sum_{i = 1}^{N!}sign(\pi_i) \prod_{n=1}^N{a_{n,\pi_i(n)}}$$ Explanation:
- The dimension of the matrix is $N$.
- The number of permutations $\pi$ (orderings) for $N$ elements is $N!$  
- $sign(\pi_i)$ is the parity of the permutations. We count the number of swaps needed to create the permutation. 1 is an even amount of swaps, -1 for an odd number.
- The product sample the relevant column $pi_i(n)$ according to the permutation
- So in words:
  *"for each permutation, sample each row with the relevant columns, sum over all permutations"*

### Properties
1. $det(A)=det(A^T)$
2. If $A$ is triangular then $det(A)$ is the product of all the elements of the triangular.
3. Swapping columns flips the sign of $det(A)$
4. If 2 rows are the same $det(A) = 0$
5. Multiplying a row / column - multiples the determinant
6. Adding Multiple of a row to another row does not affect the determinant.
7. If A is singular $det(A)=0$
8. $det(A)=0$ implies $A$ is singular.
9. $det(AB) = det(A)det(B)$ 