### A Linear Operator that Operates on a Partial Change
- With differential $df$ we calculate the local changes in $f$ when some element it depends on changes.
- The derivative is the linear operator that operates on that change.
- In the same manner, if we calculate $df$ with respect to a change in only some of its elements (or even just a single scalar) then we get a linear operator which is the partial derivative.
### Deducing Partial Derivative From Differentials
- Sometimes we have an expression involving differentials and we wish to extract a partial derivative: $df = f'(p)[dp] \rightarrow \frac {\partial f}{\partial p_i}$  
- To evaluate this, simply replace $dp$ with a partial change $dp_i$ 
- To obtain the partial derivative, you need to extract a linear operator that operates on $[dp_i]$ 



### Examples
1. $f(A, x) = A^{-1}x \rightarrow f_A?, f_x?$
   - to evaluate this, we will treat each component as constant and calculate $df$
   - $x$ constant: 
	   - $df = -A^{-1}dA\,A^{-1}x$
	   - $f_A = -A^{-1}[operand]\,A^{-1}x$ // this is a linear operator
   - $A$ constant:
	   - $df = A^{-1}dx$
	   - $f_x = A^{-1}$ // this is a linear operator - a Jacobian matrix
   - sdf
    
2. fdgd



- differentials are more flexible and easy to work with
- But sometimes we have an expression involving differentials and we wish to extract a partial derivative: $df = f'(p)[dp] \rightarrow \frac {\partial f}{\partial p_i}$  
- we can't just divide the thing. a differential is a linear operator operating on a vector / matrix.
- dividing by one element won't give us the partial derivative. we need to:
  1. calculate $f'(p)[dp_i]$ where $dp_i$ is zero vector in all places but the entry $i$.
  2. divide by the scalar $dp_i$ and take a limit
  3. This is equivalent of taking a partial derivative.
