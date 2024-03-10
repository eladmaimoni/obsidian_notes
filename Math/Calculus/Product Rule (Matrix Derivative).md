
When using differentials, our general approximation is:
$$
f(x + dx) = f(x) + f'(x)dx
$$ 
where $f'(x)$ is the linear operator that approximates the function near $x$ 

with the product rule
$$
f(x) = g(x)h(x)
$$
$$
df = g(x + dx)h(x+dx) - g(x)h(x) 
$$
now if we plug in our approximation for $g$ and $h$ we get:

$$
df = g(x)h'(x)dx + g'(x)dx\,h(x) + g'(x)dx\,h'(x)dx
$$
The last term can be dropped out for the approximation, and we get the product rule. Note that this variation will work also when the variables are vectors or matrices. This is why we didn't assume elements can commute.

$$
df = g(x)dh + dg\,h(x)
$$
