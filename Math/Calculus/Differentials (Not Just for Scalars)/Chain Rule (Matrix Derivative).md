### Derivation
$$
f(x) =g(h(x))
$$
$$
df = g(h(x+dx)) - g(h(x)) = g(h(x) + h'(x)dx) - g(h(x))
$$

If we denote:
- $y = h(x)$
- $dy = h'(x)dx$
Then:
- $df = g(y+dy)-g(y)=g'(y)[dy]$
And Finally:
- $df = g'(h(x))[h'(x)dx]$
And in the most Flexible Form:
$$
df = g'(h(x))[dh]
$$

### A Linear Operator, Not Multiplication
- We need to be careful when writing things such as  $df = g'(h(x))h'(x)dx$
- It might seems that we are **multiplying** $g'$ with $dh$. This is only the case with **scalars**.
- In the general case $g'$ is the **linear operator** that operates on $dh$.

### Hierarchical Calculation
 - A lot of times, $f$ depends on various arguments that depend on other arguments recursively.
 - With the Chain Rule, we can work ourselves down until we reach the bottom

### Examples

1. $f(p) = A^{-1}(p)$ 
   - We can say $h(p) = A(p)$ and $g(A) = A^{-1}$ and apply the chain rule.
	   - $g'(A) = -A^{-1}[operand]A^{-1}$
	   - $dh = A(p + dp) - A(p) = A'(p)[dp]$ // this needs to be evaluated per the expression
	    Note: this is NOT simply $A(dp)$ unless $h$ is linear with respect to $p$
   - Another approach (which is almost the same) is to say
     - Calculate $df$ with respect to changes in $A$: $df = -A^{-1}dA\,A^{-1}$
     - Then calculate $dA$, substituting whatever the result is with some expression that depends on $dp$: $A'(p)[dp]$
     - Note that it didn't seemed like we evaluated the chain rule, but essentially we did.
     
 2. 
    
