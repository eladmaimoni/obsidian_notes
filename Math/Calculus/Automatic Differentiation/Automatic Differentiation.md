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
- if we choose a different $d\vec{x}$, we get the Gradient / Jacobian multiplication with $d\vec{x}$
# Forward Mode
- here we start with the **innermost** functions on the left and feed it the differential.
- This is like applying the chain rule **unintuitively** from inner to outer.
- But for computational graph it is much easier, since we start with the simplest differential of the "trivial" function.
# Reverse Mode
- Here we start from the outermost function.
- With a move backward in the graph, we gradually calculate the differential with respect to a more inner variable until we reach the roots which are the variables we want.
### Example 1
$$y = v_5\Bigg(v_4\bigg(v_1(x_1),v_2(x_1, x_2)\bigg), v_3(x_2)\Bigg)$$
##### Insights:
- At every step of the way, we can always view $dy$ as:
  $dy = (\text{linearization of y with respect to changes in }v)[\text{changes in }v]$
  Or:
  $dy = \frac {\partial y}{\partial v}[dv]$
- $v$ represent the set of all variables in the same "depth" in the computational graph.
- If you are struggling to see this, here are 2 ways you can express $y$:
	- $y = f_1(v_3,v_4) \rightarrow dy = \frac {\partial f_1}{\partial v_3}[dv_{3,4}] + \frac {\partial f_1}{\partial v_4}[dv_{3,4}]$ 
	- $y = f_2(x_1, x_2) \rightarrow \frac {\partial f_2}{\partial x_1}[dx] + \frac {\partial f_2}{\partial x_2}[dx]$
- Remember that whet you write $f_2(x_1, x_2)$ you could always say $f(\vec{x}$) and write the derivatives, which are linear operators as a single combined operator $\frac {\partial f_2}{\partial \vec{x}}$ that works on the concatenation of these variables.
- Linear operators, like derivatives, behave so that you could write $\frac {\partial f_2}{\partial \vec{x}} = \frac {\partial f_2}{\partial {x_1}}  + \frac {\partial f_2}{\partial {x_2}}$ 

##### Operation Principles
- AD recursively calculates the derivatives (linear operators) of the output $y$ with respect to an inner parameter. It works for the outermost variable $v_5$ to the outermost $x_1, x_2$. 
- It further utilizes the fact that linear operators behave the way they do $L[x] = L_1[x] + L_2[x]$.
- When running the algorithm, we can add the linear operator operand $[dv]$ at each step, but this really becomes tedious once we understand the principle. when we reach the graph leaves we will have $[dx]$ as the operand 
##### Step by Step
Level 1, $y = v_5$
1. $dy = \frac {\partial y} {\partial v_5}[dv_5] = 1$ 
Level 2, $y = v_5(v_{3,4})$
3. $\frac {\partial y} {\partial v_4} = \frac {\partial v_5} {\partial v_4}[dv_{3,4}]$
+
4. $\frac {\partial y} {\partial v_3} = \frac {\partial v_5} {\partial v_3}[dv_{3,4}]$
Level 3, $y = f(v_4(v_1,v_2),v_3) \rightarrow f' = \frac {\partial y}{\partial v_4} +  \frac {\partial y}{\partial v_3}$
5. $\frac {\partial y} {\partial v_1} = \frac {\partial y} {\partial v_4}[\frac {\partial v_4} {\partial v_1}]$ // $[dv ...]$
+
6. $\frac {\partial y} {\partial v_2} = \frac {\partial y} {\partial v_4}[\frac {\partial v_4} {\partial v_2}]$
Level 4
7. $\frac {\partial y} {\partial x_1} = \frac {\partial y} {\partial v_1}[\frac {\partial v_1} {\partial x_1}] + \frac {\partial y} {\partial v_2}[\frac {\partial v_2} {\partial x_1}]$
8. $\frac {\partial y}{ \partial x_2} = \frac {\partial y}{\partial v_3}[\frac {\partial v_3}{\partial x_2}] + \frac {\partial y} {\partial v_2}[\frac {\partial v_2} {\partial x_2}]$


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

Notes:
- $dy$ or $dv_2$ which are differentials. these are actual changes after linearization of a certain function.
- the partials $\frac {\partial y} {\partial v_i}$ are the linear operators, and they are calculated analytically.

     