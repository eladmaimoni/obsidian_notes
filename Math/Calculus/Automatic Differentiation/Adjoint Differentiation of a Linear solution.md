### Problem Definition
- We have a vector of parameters $\vec{p}$ that determines the structure of a parameter matrix $A(\vec{p})$ 
- $\vec{x}(\vec{p})$ is the solution to the system $Ax=b$ that characterizes 'how the system behaves' ($p$ is the parameters that define the system behavior, $x$ is how the system behaves)
$$A(\vec{p})\vec{x}=b$$
- $f(\vec{x})$ is our scalar 'cost' function that determines how well the system behaves.
- We wish to calculate the gradient of $f$ for the purpose of optimization.
- This basically means computing $\frac{\partial f}{\partial{p_k}}$ for all elements of $\vec{p}$.  
$$f(\vec {p}) = f(A^{-1}(\vec{p})b)$$
### General Method

1. Compute the differential $df$ at our current point $\vec{p}$ according to the chain rule: $df = -f'(x)A^{-1}dA\,A^{-1}b$  
2. In our case, $dA = d(A(\vec{p}))$. This is a complex term on its own right (its not simply $A(d \vec{p})$ since we don't know if $A$ behaves linearly with respect to $p$).
3. But, computing the partials $\frac {\partial A(\vec{p})}{\partial p_k}$ is relatively easy - simply the partial derivative of each element $a_{ij}$.
4. So we can compute the gradient components $\frac {\partial f}{\partial p_k} = -f'(x)A^{-1} \frac {\partial A}{\partial p_k}\,A^{-1}b$  
5. Note that $\vec{x} = A^{-1}(\vec{p})b$ so that
   $$\frac {\partial f}{\partial p_k} = -f'(x)A^{-1} \frac {\partial A}{\partial p_k}\,\vec{x}$$  
### Adjoint Differentiation
- The point is to show that we can compute $\nabla f$ at each point $\vec{p}$ efficiently by reducing the amount of computations we do per partial derivatives.
- Calculations that are uniform across all partials:
	1. Solving a linear equation to get $\vec{x} = A^{-1}(\vec{p})b$
	2. Computing the gradient of $f$ at point $\vec{x}$
	3. Solving another equation - computing the vector $v^T = -f'(x)A^{-1}$ which is equivalent to solving the equation $A^Tv = f'(x)$ 
- Per partial we are left with
	1. Evaluating $\frac {\partial A(\vec{p})}{\partial p_k}$ 
	2. Multiplying $v^T(\frac {\partial A(\vec{p})}{\partial p_k} \vec{x})$ 
### Why is this a thing?
- Note we first calculated the outermost differential (the last step in the network)
- Every time you see an expression involving $A^{-1}$ you need to realize that we don't compute $A^{-1}$ (this is expensive, and requires an extra multiplication afterwards) but instead solve a linear set of equations that evaluates the term containing $A^{-1}$. 
- If we avoid pre calculating $v^T$ and computing and calculate the innermost function first:
     $$\frac {\partial f}{\partial p_k} = -f'(x) \LARGE(A^{-1} \frac {\partial A}{\partial p_k}\,\vec{x}\LARGE)$$
- In order to evaluate the innermost term we would have to solve an equation per partial derivative, which is expensive.