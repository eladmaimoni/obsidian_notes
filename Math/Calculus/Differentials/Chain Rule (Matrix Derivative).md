   $$
f(x) =g(h(x))
$$
$$
df = g(h(x+dx)) - g(h(x)) = g(h(x) + h'(x)dx) - g(h(x))
$$

if we denote:
- $y = h(x)$
- $dy = h'(x)dx$
then:
$$
df = g(y+dy)-g(y)=g'(y)[dy]
$$
or:
$$
df = g'(h(x))[dh]
$$
$$
df = g'(h(x))[h'(x)dx]
$$

Note:
- We need to be careful when writing things such as  $df = g'(h(x))h'(x)dx$
- It might seems that we are **multiplying** $g'$ with $dh$. This is only the case with **scalars**.
- In the general case $g'$ is the **linear operator** that operates on $dh$.

Additional Notes:
- in many cases, we have a complex function $g(h(x))$ and we already know $dg$ and $g'$ in case it didn't have $h(x)$ as a parameter.
- one naive way is to reapply the chain rule. 
- but we need to understand that the chain rule simply says: 
  ***evaluate the linear operator $g'$ at $h(x)$, and apply it on $dh$***
- example: 
	- $f(p) = A^{-1}(p)$ 
	- we can say $h(p) = A(p)$ and $g(A) = A^{-1}$ and apply the chain rule.
	- but, we can also use the fact that $dg = -A^{-1}dA\,A^{-1}$ [[Inverse of a Matrix]]   
	- this is a linear operator, so we simply say $df = -A^{-1}(p)d(A(p))\,A^{-1}(p)$  
	- $d(A(p))$ is simply $A(dp)$
	- 