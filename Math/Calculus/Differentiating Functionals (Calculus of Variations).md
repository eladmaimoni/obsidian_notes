- How do we differentiate with respect to a function parameter?
- What does it mean $f(u + du) - f(u)$ whn $u$ is a function?
- What does $du$ mean when $u$ is a function?
  - it is a small perturbation relative to the norm defined on the functions (functions are vectors). 
# Functionals
- a function that takes another function as a parameter and outputs a number.
### Example
$$f(u(x)) = \int_{0}^{1} sin\big(u(x)\big)dx$$
### Calculating Differential of a Functional
$$df(u(x)) = \int_{0}^{1} {\Big[sin\big((u(x) + du(x)\big) - sin\big(u(x)\big)\Big]dx}$$      
- In order to calculate $df$ we need to linearize $f(u + du)$
- usually we linearize the function we differentiate (taylor apporx up order 1)
- here we have an integral and an integrand - what do we linearize exactly? Not super clear.
  I think the answer is that we linearize the function $f(u + du)$ around function $u$. so it will be linear with respect to $du$. the integration is a linear operator on functions, but the sin is not.
  so if we linearize the sin part, the whole thing becomes linear to with respect to $du$  
- $sin(u(x) + du(x)) = sin(u(x)) + cos(u(x))du(x)$ 
- The end Result:
$$df(u(x)) = \int_{0}^{1} {cos\big((u(x)\big)du(x)dx}$$
	Which is linear with respect to $du$.
 