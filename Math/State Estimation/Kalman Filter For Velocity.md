### Sum of independent normally distributed variables
- Is also a normally distributed variable
- The mean is the sum of the means
- The variance is the sum of the variances
- [https://en.wikipedia.org/wiki/Sum_of_normally_distributed_random_variables](Wiki)
This fact is used throughout the equations for the Kalman filter, especially when we combine variances. 

# Assuming Constant Velocity
### Prediction
- We **predict** that our velocity doesn't change and hence its uncertainty doesn't change.
  $\hat{\dot{x}}_{n, n-1} = \hat{\dot{x}}_{n-1, n-1}$ 
  $\big(\sigma^{v}_{n,n-1}\big)^2 = \big(\sigma^{v}_{n-1,n-1}\big)^2$ 
- We **predict** that our position changes accordingly:
  $\hat{x}_{n,n-1} = \hat{x}_{n-1,n-1} + \hat{\dot{x}}_{n-1,n-1}\Delta t$ 
  $\big(\sigma^{x}_{n,n-1}\big)^2 = \big(\sigma^{x}_{n-1,n-1}\big)^2 + \big(\sigma^{v}_{n-1,n-1}\Delta t\big)^2$
- 
### Update
- Given a new measurement, we wish to mix it with the prediction.
- Our new estimate is a weighted sum of the measurement and the prediction:
  $\hat{x}_{n,n} = w_xz_n + (1-w_x)\hat{x}_{n, n-1}$
  $\big(\sigma^{x}_{n,n}\big)^2 = w_x^2\big(\sigma^{z_n}\big)^2 + (1-w_x)^2\big(\sigma^{x}_{n,n-1}\big)^2$
- The ideal weight $w_x$ is the one that minimizes the uncertainty $\big(\sigma^{x}_{n,n}\big)^2$ 
  $w_x = \frac {(\sigma^{x}_{n,n-1})^2} {(\sigma^{x}_{n,n-1})^2 + (\sigma^{z_n})^2}$ 
- 