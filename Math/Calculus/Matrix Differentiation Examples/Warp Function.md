$$

R(\theta) =
\begin{pmatrix}
cos(\theta) & sin(\theta) \\
-sin(\theta) & cos(\theta)
\end{pmatrix}
$$
$$
wrap(\vec{x}) = R(\theta\|\vec{x}\|)\vec{x}
$$
Lets analyze the structure of this function:
- $g(x) = R(x)$ (scalar to matrix)
- $h(\vec{x}) = \theta\|\vec{x}\| = \theta \sqrt{\vec{x}^T\vec{x}}$ (vector to scalar)
- $f(\vec{x}) = g(h(\vec{x}))$ (vector to matrix)
We can also further analyze the function $h$:
- $h_2(\vec{x}) = \vec{x}^T \vec{x}$ (vector to scalar)
- $h_1(x) = \theta \sqrt{x}$ (scalar tp scalar)
- $h(\vec{x}) = h_1(h_2(\vec{x}))$ (vector to scalar)
And our final function:
- $w(\vec{x}) = f(\vec{x})\vec{x}$ (vector to vector)

### 1 - Product Rule for $w$
It is a multiplication of a matrix $g(\vec{x})$  by a vector $\vec{x}$. This is a product between 2 functions of $\vec{x}$.  even though this is a product between functions that are not of the same shape - one is a matrix and one is a vector, we can apply the [[Product Rule (Matrix Derivative)]]. this is because the way the product rule is derived don't care about the actual elements involved as long as the behave like standard multiplication. 


$$
dw = f(\vec{x})d\vec{x} + df\vec{x}
$$
## 2 - Chain Rule for $f$
- to calculate $df$ we can apply the [[Chain Rule (Matrix Derivative)]]:

$$
df = g'(h(\vec{x})) h'(\vec{x}) d\,\vec{x}  
$$

- $g'(\phi) = \begin{pmatrix} -sin(\phi) & cos(\phi) \\ -cos(\phi) & -sin(\phi) \end{pmatrix}$ 

## 3 - Chain Rule for $h$
- $dh_2 = d(\vec{x}^T \vec{x}) = 2\vec{x}^Td\vec{x}$  (we can use the product rule, or the definition here)  
- $dh_1 = \frac {\theta dx} {2\sqrt{x}} = h_1'(x)dx$ (scalar differential)
- $dh = h_1'(h_2(\vec{x}))dh_2 =\frac {\theta} {\|\vec{x}\|} \vec{x}^Td\vec{x}$  


## finally

$$
dw = R(\theta \|\vec{x}\|)d\vec{x} + R'(\theta \|\vec{x}\|) \frac {\theta} {\|\vec{x}\|} \vec{x}^Td\vec{x} \, \vec{x}
$$

Note that $\vec{x}^Td\vec{x}$ is a scalar and can be swapped to the end of the term to get an expression multiplied by $d\vec{x}$  