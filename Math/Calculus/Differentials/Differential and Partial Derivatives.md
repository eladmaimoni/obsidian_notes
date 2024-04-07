- differentials are more flexible and easy to work with
- But sometimes we have an expression involving differentials and we wish to extract a partial derivative: $df = f'(p)[dp] \rightarrow \frac {\partial f}{\partial p_i}$  
- we can't just divide the thing. a differential is a linear operator operating on a vector / matrix.
- dividing by one element won't give us the partial derivative. we need to:
  1. calculate $f'(p)[dp_i]$ where $dp_i$ is zero vector in all places but the entry $i$.
  2. divide by the scalar $dp_i$ and take a limit
  3. This is equivalent of taking a partial derivative.