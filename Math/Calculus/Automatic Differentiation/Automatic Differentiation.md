 # Idea
- Take a large complex function $f(\vec{x})$ and represent it as a computational graph of elementary operations - just like we do when we structure a complex function in order to apply the chain rule.
- Each Node in the graph is an elementary scalar function (for example $v_2 = cos(v_1)$ or $v_3 = v_1v_2$).
- The graph flows left to right (input to output).
  - left side nodes - innermost functions (operate first).
  - right side node - outermost functions (operate last).
  - the leftmost nodes are simply the input values $\vec{x}$ (you can think of this as a function $f(\vec{x} )= \vec{x}$ and hence its differential is simply $d\vec{x}$. 
- The idea is to feed the graph with ***differentials*** and obtain the output differential.

# Dual Numbers
- the idea is to replace $x$ as an input to the graph with dual $(\vec{x}, d\vec{x})$.
- $\vec{x}$ is an input value, propagating it through the graph will yield the value at a certain point.
- $d\vec{x}$ is a differential, and it propagates through the graph by using the **differential rules**. This can be though of as "operator overloading".
- if we choose a value for $d\vec{x}$ . propagating it through the graph yield the value of the linear local approximation of $f$ as it is applied to $d\vec{x}$: $d\vec{y} = f'(\vec{x})[d\vec{x}]$.
- for scalar valued functions $f(\vec{x}) = y$, $f'$ is the gradient.
- for vector valued functions, $f(\vec{x}) = \vec{y}$, $f'$ is the Jacobian matrix.
- if we choose $d\vec{x} = e_i$ we can obtain an element of the gradient or column of the Jacobian.
- if we choose and other $d\vec{x}$, we get the Gradient / Jacobian multiplication with $d\vec{x}$
# Forward Mode
- here we start with the **innermost** functions on the left and feed it the differential.
- This is like applying the chain rule **unintuitively** from inner to outer.
- But for computational graph it is much easier, since we start with the simplest differential of the "trivial" function.
# Reverse Mode
- Here we start from the outermost function.
- With a move backward in the graph, we gradually calculate the differential with respect to a more inner variable until we reach the roots which are the variables we want.
### Example
$$y = v_5\Bigg(v_4\bigg(v_1(x_1),v_2(x_1, x_2)\bigg), v_3(x_2)\Bigg)$$
- Let's examine the differential $dy$ as it is affected by $dv_2$:
  - $v_2$ directly affects the output of the function $v_4$.
  - hence we can describe the differential as:
   $dy = (\text{linearization of y with respect to changes in }v_4)[\text{changes in }v_4]$
   $dy = \frac {\partial y} {\partial v_4} [dv_4]$   
  - $dv_4 = \frac {\partial v_4} {\partial v_1}[dv_1] + \frac {\partial v_4} {\partial v_2}[dv_2]$
  - so combined together we can obtain:
    $dy = \frac {\partial y} {\partial v_4} \big[\frac {\partial v_4} {\partial v_1}[dv_1] + \frac {\partial v_4} {\partial v_2}[dv_2]\big]$  
  - since we are talking scalar functions here, this translates to multiplications.
  - we can see how we can apply this rule recursively from the output until we reach $x$:
    1. $\frac {\partial y} {\partial v_5} = 1$ 
    2. $\frac {\partial y} {\partial v_4} = \frac {\partial v_5} {\partial v_4}$
    3. $\frac {\partial y} {\partial v_3} = \frac {\partial v_5} {\partial v_3}$
    4. $\frac {\partial y} {\partial v_1} = \frac {\partial y} {\partial v_4}[\frac {\partial v_4} {\partial v_1}]$
    5. $\frac {\partial y} {\partial v_2} = \frac {\partial y} {\partial v_4}[\frac {\partial v_4} {\partial v_2}]$
    6. $\frac {\partial y} {\partial x_1} = \frac {\partial y} {\partial v_1}[\frac {\partial v_1} {\partial x_1}] + \frac {\partial y} {\partial v_2}[\frac {\partial v_2} {\partial x_1}]$

Notes:
- $dy$ or $dv_2$ which are differentials. these are actual changes after linearization of a certain function.
- the partials $\frac {\partial y} {\partial v_i}$ are the linear operators, and they are calculated analytically.

     