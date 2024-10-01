### Sum of independent normally distributed variables
- Is also a normally distributed variable
- The mean is the sum of the means
- The variance is the sum of the variances
- [https://en.wikipedia.org/wiki/Sum_of_normally_distributed_random_variables](Wiki) 
This fact is used throughout the equations for the Kalman filter, especially when we combine variances. 


Key points:
- with no process noise, each measurement, even if noisy, decrease the uncertainty.
- so no process noise means that uncertainty will always decrease
- 
# Assuming Constant Velocity
### Prediction
- We assume that our velocity doesn't change. So the model predict the new position and velocity according to the current velocity (n-1)
  $\hat{\dot{x}}_{n, n-1} = \hat{\dot{x}}_{n-1, n-1}$ 
  $\hat{x}_{n,n-1} = \hat{x}_{n-1,n-1} + \hat{\dot{x}}_{n-1,n-1}\Delta t$
- When we consider the variance, the predicted velocity has the same variance as the current velocity (they are the same random variable representing the velocity)
  $\big(\sigma^{v}_{n,n-1}\big)^2 = \big(\sigma^{v}_{n-1,n-1}\big)^2$ 
- The predicted position is a sum of 2 random variable, and hence the variance is the sum of variances.
  $\big(\sigma^{x}_{n,n-1}\big)^2 = \big(\sigma^{x}_{n-1,n-1}\big)^2 + \big(\sigma^{v}_{n-1,n-1}\Delta t\big)^2$
Intuition:
- The predicted position uncertainty actually increases, especially for large $dt$.
- What happens when we initialize the system? We initialize the variances with some number - this is the initial state uncertainty.
### Update
- Given a new measurement, we wish to mix it with the prediction.
- Position estimate is a weighted sum of the measurement and the prediction:
  $\hat{x}_{n,n} = w_xz_n + (1-w_x)\hat{x}_{n, n-1}$
  $\big(\sigma^{x}_{n,n}\big)^2 = w_x^2\big(\sigma^{z_n}\big)^2 + (1-w_x)^2\big(\sigma^{x}_{n,n-1}\big)^2$
- Velocity Estimate
  measured velocity: $v_n = \frac {z_n - \hat{x}_{n-1,n-1}}{\Delta t}$
  $\big(\sigma^{v_n}\big)^2 = \frac {\big(\sigma^{z_n}\big)^2 +\big(\sigma^{x}_{n-1,n-1}\big)^2}{\Delta t^2}$ 
  $\hat{\dot{x}}_{n,n} = w_v v_n + (1-w_v)\hat{\dot{x}}_{n, n-1}$
  $\big(\sigma^{v}_{n,n}\big)^2 = w_v^2\big(\sigma^{v_n}\big)^2 + (1-w_v)^2\big(\sigma^{v}_{n,n-1}\big)^2$
  
- Our new variance is updated accordingly
- The ideal weights $w_x, w_v$ are the ones that minimizes the uncertainty $\big(\sigma^{x}_{n,n}\big)^2$ 
  $w_x = \frac {(\sigma^{x}_{n,n-1})^2} {(\sigma^{x}_{n,n-1})^2 + (\sigma^{z_n})^2}$ 
  $w_v = \frac {(\sigma^{v}_{n,n-1})^2} {(\sigma^{v}_{n,n-1})^2 + (\sigma^{v_n})^2}$ 
- If we substitute the expression for the ideal weights we obtain the following equations for the new variances:
    $\big(\sigma^{x}_{n,n}\big)^2 = (1-w_x)\big(\sigma^{x}_{n,n-1}\big)^2$
    $\big(\sigma^{v}_{n,n}\big)^2 = (1-w_v)\big(\sigma^{v}_{n,n-1}\big)^2$
  