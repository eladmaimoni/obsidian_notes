- In the linear solution case, we tried to optimize $f(\vec{x})$ where $\vec{x}$ is a solution of a linear equation that depends on the system parameters $\vec{p}$: $A(\vec{p})\vec{x} = b$ 
- In the nonlinear case, $\vec{x}$ is the solution of some non linear equation $g(\vec{x}, \vec{p}) = \vec{0}$.
- Again we wish to optimize $f(\vec{x})$.
### General Method
1. solve $g$ in order to evalute $x$. this usually involve using a non linear solver
2. compute the differential $df = f'(\vec{x})dx$ 
3. $dx$ is evaluated from the differential $dg$ at the point which defines $\vec{x}$ which is the root of $g(\vec{p}, \vec{x})$ 
   $dg = \vec{0} = \frac {\partial g}{\partial p} dp + \frac {\partial g}{\partial x} dx = J_pdp + J_x dx$ 
   - $dg = 0$ since this is how $\vec{x}$ is defined.
   - Note that we could have written this using a single Jacobian, but separating this into 2 Jacobians is equivalent (multiplying 1 matrix by p and the other by x vs 1 concatenated matrix multiplied by the concatenation of x and p)
4. $dx = -J_x^{-1}J_pdp$ 
5. $df = - (f'(x) J_x^{-1}) J_pdp$ 
### Adjoint Differentiation
- Lets go through the computational steps to compute $\nabla f$.
- Uniform calculations:
  1. solve $g = 0$ to evaluate $x$
  2. compute $f'(x)$ 
  3. evaluate the left term (adjoint vector) by solving $J_x^Tv=f'(x)$ 
  4. multiply some matrices.
- So bottom line: non linear solution to obtain $x$, another linear solution to obtain $v$ 
