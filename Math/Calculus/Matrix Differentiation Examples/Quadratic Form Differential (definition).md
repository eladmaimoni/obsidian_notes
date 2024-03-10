$$
f(\vec{x}) = x^TAx
$$

$$
df = f(x + dx) - f(x) = x^TAx + x^TAdx + dx^TAx +dx^TAdx-x^TAx 
$$
now
- we assume the quadradic term $dx^TAdx$ is small and can be neglected
- we know that quadradic form is a scalar and can be transposed liberally: $dx^TAx = x^TA^Tdx

$$
df = x^T(A+A^T)dx
$$