$$f(A) = det(A)$$
Gradient Form
$$\nabla f = det(A)A^{-T}$$
Other Gradient Forms
- $cofactor(A)$  - if you remember how to compute the determinant manually (take a row, cross the elements, compute the determinant of what is left), then the cofactor $C_{ij}$ is the determinant of the submatrix when we cross out row $i$ and column $j$.
- $adj(A^T)$ (remember that the adjoint of a matrix $A$ is $det(A)A^{-1}$ and the transpose does not affect the determinant)

Differential Form
$$df = \nabla f \cdot dA = trace(det(A)A^{-1}dA)$$
Other Differential forms:
- $trace(adj(A)dA)$

### Proof using cofactors
- consider how you compute the determinant using cofactors of row $i$:
  $det(A) = a_{i1}C_{i1} + a{i2}C_{i2} + ... a_{in}C_{in}$ 
- Computing partial derivatives:
  $\frac {\partial det(A)}{\partial a_{ij}} = C_{ij}$ 
- Now we can write:
  $df = vec(C) \cdot vec(dA) = trace(C^TdA) = \langle C,dA \rangle$     
- and hence $\nabla f = C$ 

### Proof using tricks
- let's evaluate the term $det(I + dA)$.
- If you remember the determinant definition, it is the sum of $N!$ permutations, each permutation multiplies the samples of 1 element per row.
- The only permutation that creates a product where there are terms which are not high order (>2) terms of the elements of $dA$ is the permutation that chooses the diagonal elements.
- hence $det(I+dA) = \prod(1+dA_{ii}) = 1 + trace(dA)$ after neglecting higher order terms.
- Note, any permutation that does not choose all its elements on the diagonal, has at least 2 non diagonal elements and hence neglected.

$det(A + dA) = det(A + A(A^{-1})dA) = det(A)det(I + A^{-1}dA)$  
