### - $A \bigotimes B$ eigenvalues are the multiplicative permutation of $A$'s and $B$'s eigenvalues 


Uses:
- [[Kronecker Product Properties#Mixed Product $(A bigotimes B)(C bigotimes D) = AC bigotimes BD$ | Mixed Product]]  $AC \bigotimes BD = (A \bigotimes B)(C \bigotimes D)$ 
- [[Shur Decomposition]] every matrix is unitarily similar to an upper triangular matrix with the matrix eigenvalues on the diagonal

Proof

1. construct the Shur Decomposition of both matrices
$$
\begin{gather}
T_1 = Q_1^TAQ_1 \\ 
T_2 = Q_2^TBQ_2 \\
\end{gather}
$$
2. Multiply the decomposition, use the mixed product rule
$$
T_1 \bigotimes T_2 = Q_1^TAQ_1 \bigotimes Q_2^TBQ_2 = (Q_1^T \bigotimes Q_2^T)(AQ_1\bigotimes BQ_2) = (Q_1^T \bigotimes Q_2^T)(A\bigotimes B)(Q_1 \bigotimes Q_2)
$$
3. Notice that:
	- $T_1 \bigotimes T_2$ has the permutations $\lambda_i \mu_j$ on its diagonal
	- $(Q_1^T \bigotimes Q_2^T)$ and $(Q_2^T \bigotimes Q_2^T)$ are both unitary and the inverse of each other (mulitply them by each other to get $I$ )
	
	


#math/matrix #math/eigenvalues