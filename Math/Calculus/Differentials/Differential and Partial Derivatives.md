### What Are Partial Derivatives?
- With differential $df$ we calculate the local changes in $f$ when some element it depends on changes.
- The derivative is the linear operator that operates on that change.
- In the same manner, if we calculate $df$ with respect to a change in only some of its elements (or even just a single scalar) then we get a linear operator which is the partial derivative.

### Deducing changes in 



- differentials are more flexible and easy to work with
- But sometimes we have an expression involving differentials and we wish to extract a partial derivative: $df = f'(p)[dp] \rightarrow \frac {\partial f}{\partial p_i}$  
- we can't just divide the thing. a differential is a linear operator operating on a vector / matrix.
- dividing by one element won't give us the partial derivative. we need to:
  1. calculate $f'(p)[dp_i]$ where $dp_i$ is zero vector in all places but the entry $i$.
  2. divide by the scalar $dp_i$ and take a limit
  3. This is equivalent of taking a partial derivative.
