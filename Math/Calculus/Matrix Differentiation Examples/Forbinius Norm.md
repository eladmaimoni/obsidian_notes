$f(A) = \|A\|_F = \sqrt{trace(A^TA)}$ 

- $g(x) = \sqrt{x} \rightarrow dg = \frac {dx} {2\sqrt{x}}$    
- $h(A) = trace(A^TA)$
- $df = g'(h(A))[dh]$
### Calculating $dh$:
- use the chain rule: $h'(A^TA)[d(A^TA)]$ which is a bit hard to grasp since $h'$ is not easily calculated for a trace.
- look at the definition of the differential: $dh = trace(B + dB) - trace(B) = trace(dB)$ 
- so $h'$ is simply a linear operator over the differential ($dB$), and its the same at any point (even at $A^TA$ in this case)
- so $dh = trace(A^TdA + dA^TA))$ 

# Applying the chain rule
$$df = g'(h(A))[dh] = \frac {trace(A^TdA + dA^TA))} {2\sqrt{trace(A^TA)}}$$
if we use the fact that $trace(A + B) = trace(A) + trace(B)$ and $trace(A) = trace(A^T)$ then we get:
$$
df = \frac {A^TdA} {\|A\|_F}
$$
which is somewhat like a dot product of the gradient $\frac {A} {\|A\|_F}$ with $dA$
