
given $A$ is a square matrix:
$$
f(A) = A^3
$$
we will calculate $df$ using the [[Product Rule (Matrix Derivative)]] 

$$
df = g(A)dh + dg\,h(A)
$$
- $g(A)=A$, $h(A)=A^2$
- $dg = dA$ (this can be seen using the definition of the differential)
- $dh = AdA + dA\,A$ (this also uses the product rule)

After putting in all the variables:

$$
df = A^2dA + A\,dA\,A + dA\,A^2
$$

Note that this is still a **linear operator** that acts on $dA$ even though it is not a simple multiplication of something by $dA$.
To see the linearity, you can multiply $dA$ by a scalar or add an element to $dA$ that is behaves linearly:

$$
L(dA) = A^2dA + A\,dA\,A + dA\,A^2
$$
$$
L(a_1\cdot dA_1 + a_2 \cdot dA_2) = a_1L(dA_1) + a_2L(dA_2)
$$

Remember that $dA$ is just a "small matrix" perturbation