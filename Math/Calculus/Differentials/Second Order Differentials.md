- The differential $df$ is the result of a linear operator - the derivative $f'(x)$, as it operates on a small change $dx$: $df = f'(x)[dx]$.
- The second order differential, is the differential of $df$:$$d(df) = f'(x + dx')[dx] - f'(x)[dx] = f''(x)[dx'][dx]$$
- This is a **Bi**linear operator - an operator that is linear in 2 arguments. it is the difference of 2 linear operators.
- $dx'$ - the change in **where** we are taking the derivative
- $dx$ - the change in where we are evaluating our function~~
- Bilinearity - $B[u_1 + u_2, v] = B[u_1, v] + B[u_2, v]$ (same for the second argument)
- Generally the order in a bilinear operator matters $B[u,v] \neq B[v,u]$  - it may not even make sense if the args are not in the same vector space.
- But the second order derivative is a **symmetric bilinear operator**: $$f''(x)[dx',dx] = f''(x)[dx,dx']$$ 
- To see why it is symmetric we need to expand the definition from before:
  - $d(df) = f'(x + dx')[dx] - f'(x)[dx]$
  - $f'(x)[dx] = f(x+dx) - f(x)$ 
  - $f'(x+dx')[dx] = f(x + dx' + dx) - f(x + dx')$
  So: $$f(x + dx' + dx) - f(x + dx') - f(x+dx) + f(x)$$
  Which is symmetric.

- So the symmetric bilinear operator $f''(x)$ is an operator that takes in 2 vectors $[dx, dx']$ and makes them a scalar. the only linear operator that does this is a symmetric matrix. (this relies on some theorem whatever).
  So this symmetric matrix is called the Hessian: $$dx^THdx'$$ 
  - deriving the Hessian using calculus.
    $df = \nabla f \cdot dx$ 
    $d(df) = d(\nabla^T f \cdot dx)= d(\nabla^T f) \cdot dx = dx^T \cdot d(\nabla f)$ (the last transition is ok since dx is just a vector of numbers)
    $$d(\nabla f) = 
    \begin{pmatrix}
	d(\frac {\partial f}{\partial x_1} ) \\
	\vdots \\
	d(\frac {\partial f}{\partial x_n} ) \\
	\end{pmatrix}
	=
	\begin{pmatrix}
	\nabla(\frac {\partial f}{\partial x_1} )^Tdx \\
	\vdots \\
	\nabla(\frac {\partial f}{\partial x_n} )^Tdx \\
	\end{pmatrix}
	$$ and so you can see how the lines of the hessian come about and the form $dx^THdx$ 
- The Hessian is the Jacobian of the gradient
- 