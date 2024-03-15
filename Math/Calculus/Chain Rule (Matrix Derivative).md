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
- It might seems that we are multiplying the $g'$ with $dh$. This is only the case with scalars.
- In the general case $g'$ is the linear **operator** that operates on $dh$.