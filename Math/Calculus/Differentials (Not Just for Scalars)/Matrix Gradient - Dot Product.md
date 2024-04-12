- The gradient is usually computed for vector functions (vector input, scalar output)
- What about gradients of a matrix functions (matrix in, scalar out)?

Hilbert spaces
- simply vector spaces with an inner product
- inner product should have the following properties:
  
Inner Product For matrices $\langle A,B \rangle = trace(A^TB)$ 


### Examples:
1. $f(A, B) = trace(A^TBA) \rightarrow \nabla{f_A}?, \nabla{f_B}?$ ($A$ and $B$ are square matrices)
   - $B$ is constant: 
	   - $df = trace(A^TBdA + dA^TBA)$ // we used the fact that the **trace is linear**, and the product rule.
	   - we use $trace(C^T) = trace(C)$ and $trace(C+D) = trace(C) + trace(D)$ to deduce:
	     $df = trace\big(A^TBdA\big) + trace\big((BA)^TdA\big)$ 
	     $df = trace\big(A^T(B + B^T)dA)$ 
	   - In gradient form:
	     $\nabla{f_A} = (B+B^T)A$  
	   - 
   - $A$ is constant:
	   - $df = trace(A^TdBA)$
	   - we use another trace rule $trace(CD) = trace(DC)$ to deduce:
	     $df = trace(AA^TdB)$ 
	   - In gradient form:
	     $\nabla{f_B} = A^TA$ 
	   - sdfs
     
1. dfgasg