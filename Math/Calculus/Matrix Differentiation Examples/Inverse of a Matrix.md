
$$
g(A) = A^{-1}
$$
to calculate $dg$ we will do some trickery. we will differentiate the function $f(A) = A^{-1}A$ using the [[Product Rule (Matrix Derivative)]] instead:

$$
df = d(I) = 0 = A^{-1}dA + dgA
$$
and hence
$$
dg = -A^{-1}dA\,A^{-1}
$$
