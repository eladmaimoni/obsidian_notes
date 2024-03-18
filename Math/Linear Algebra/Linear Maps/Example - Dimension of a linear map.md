What is the dimension of the set of all linear maps $L$ that maps $n \times n$ matrices to $n \times n$ matrices?

- a naive answer might say that the dimension of the set of linear maps is simply $n^2$ since it consist of all the $n \times n$ matrices.
- however this is wrong.
- the way a mapping is defined is by how it acts on the bases of the space. 
- in this case the bases for the set of $n \times n$ matrices is the set of matrices with all elements zero except for one place: $1_{ij}$.
- a $n \times n$ matrix acts uniformly on all bases. but we can have a different matrix acting on each base element and it will still be a linear map: $A_{11} \cdot 1_{11} + A_{12} \cdot 1_{12} ...$  
- another way to think of it is if we vectorize the input matrix, we can act on it using a huge $n^2 \times n^2$ matrix to produce another vectorized $n \times n$ matrix. 