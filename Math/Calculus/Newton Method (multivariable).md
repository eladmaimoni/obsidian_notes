- Finding the root of a function
- Unlike Gradient Descent where we arbitrarily choose the step in the direction of the gradient, here we actually compute the 'ideal' step.
- Idea is to **linearize** the function around the guess point and compute the root of the approximation.
  $f(x + \delta x) = f(x) + f'(x)[\delta x] = 0$  
- if we can represent $f'(x)$ as a Jacobian matrix, we can compute the ideal $\delta x$ using its inverse.