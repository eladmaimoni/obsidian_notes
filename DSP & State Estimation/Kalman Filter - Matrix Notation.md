
### True State
$$x_t = F_t x_{t-1} + B_t u_t + w_t$$
### Prediction
$$x_{t,t-1} = F_t x_{t-1,t-1} + B_tu_t$$
- $x$ is our state vector - for example (position, velocity)
- $F_t$ is the state transition matrix - this is the dynamic model. 

- $B_t$ is the control input matrix. it can express how the system controls affect the state.
- $u_t$ is the control input vector.


##### Covariance Extrapolation
- We assume that our random variable $x$ is going through a linear transformation
  This equation approximate how $x$ distribution (multivariate gaussian) changes when we apply a linear transformation.
$$
P_{t,t-1} = F_tP_{t-1,t-1}F_t^T + Q_t
$$
- $P$ - the covariance matrix
- $Q$ - the process noise, this models inaccuracies in the dynamic model we chose (for example - the fact that our velocity is constant when there are no inputs).

### Update
$$x_{t,t} = (I - K_t)x_{t,t-1} + K_t z_t$$
Our new covariance matrix is:
$$
P_{t,t} = (I - K_t)P_{t,t-1}(I - K_t)^T + K_tP_zK_t^T
$$
(This is a sum of 2 independent normally distributed random variables)

To deduce $K_t$ we need to optimize the covariance to be minimal (matrix calculus)
$$
K_n = P_{t,t-1}(P_{t,t-1} + P_z)^{-1}
$$


### Crane Slew Angle Example


### Prediction
##### $B_t u_t$ - Input System
- We model the effects of the joystick input system and the natural crane deceleration
- The joystick input has a direction (sign) and gear.
- Each gear either accelerate or decelerate the jib at constant acceleration.
- Each gear can only reach a certain maximal velocity.
- Without joystick input, the crane decelerate at a constant rate.
- $d$ - The natural deceleration (either constant or a function of (velocity, wind, load) - we can model this.
- $a$ - jib acceleration - can be a function of joystick. 

    $$
  d = 
  \begin{cases}
  0 && \text{if } |\dot{x}_{t-1,t-1}| > 0 \\
  -sign(\dot{x}_{t-1,t-1}) \cdot deceleration && \text{else}
  \end{cases}
  $$

  $$
  a = 
  \begin{cases}
  sign(joystick) \cdot acceleration(gear)&& \text{if } gear > 0 \text{ AND } \dot{x}_{t-1, t-1} < v_{max}(gear) \\
  -d && \text{else if } gear > 0 \\
  0 && \text{else if } gear == 0
  \end{cases}
  $$
 

$$
B_t u_t =
\begin{pmatrix}
\frac{\Delta t^2}{2} && \frac{\Delta t^2}{2} \\
\Delta t && \Delta t
\end{pmatrix}
\begin{pmatrix}
\text{d} \\
\text{a} \\
\end{pmatrix}
$$
- we can model this just using the joystick - have $a$ equals constant deceleration factor when the gear is zero 
##### $F_t$ - state transition matrix
 $F_t = \begin{pmatrix}1 && \Delta t \\ 1 && 0\end{pmatrix}$ to express constant velocity dynamics: 
  $x_{t,t-1} = x_{t-1,t-1} + \Delta t \cdot \dot{x}_{t-1, t-1}$

### Update
- here we have a measurement covariance $P_z$ which will express the transition



### Derivation of the optimal Kalman Gain

- We wish to minimize the variance of the estimation
  $$
P_{t,t} = (I - K_tH)P_{t,t-1}(I - K_tH)^T + K_tP_zK_t^T
$$
- This means find the minimum of the trace of the covariance matrix $P_{t,t}$:
  $$
  \min_{K_t}{\big(trace(P_{t,t})\big)} 
  $$
- We will compute the differential of the trace of the covariance matrix
  $P = P_{t,t-1}$       //  $n_x \times n_x$ 
  $f = P_{t,t}$           //  $n_x \times n_x$ 
  $H$                    //  $n_z \times n_x$ 
  $K = K_t$           //  $n_x \times n_z$ 
  $\tilde{K} = I - KH$ 
  $A_1 = \tilde{K}P\tilde{K}^T$
  $A_2 = KRK^T$
- And so we wish to compute $df$ where $f = trace(A_1 + A_2) = trace(A_1) + trace(A_2)$
#### Computing $d(trace(A_1))$:
- $d(trace(A_1)) = trace(dA_1)$ // because the trace is linear
- $dA_1 = \tilde{K}P\,d\tilde{K}^T + d\tilde{K}P\,\tilde{K}^T$ 
- we use the following rules:
	- $P = P^T$ 
	- trace(C+D) = trace(C) + trace(D)
	- trace(D) = trace(D^T)
  and so:
  $dA_1 = 2 \cdot trace(d\tilde{K} P\, \tilde{K}^T)$ 
- We can now use another trace property: $trace(CD) = trace(DC)$ for compatible matrices. here all the matrices are square so:
  $dA_1 = trace(P\tilde{K}^Td\tilde{K})$ 
  $d\tilde{K} = -dKH$
  
  