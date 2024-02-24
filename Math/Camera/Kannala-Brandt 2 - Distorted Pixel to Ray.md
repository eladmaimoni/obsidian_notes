Given a distorted pixel, and known model params. 

There are 3 functions involved in forming a pixel: $A \circ D \circ F$: project, distort and scale/shift to pixel.
The reverse operation is: reverse shift/scale, undistort, and unproject: $F^{-1} \circ D^{-1}\circ A^{-1}$

### 1 - Pixel to distorted projected point (normalized coordinates)
Given a pixel $(u,v)$, we can easily obtain the distorted coordinates in normalized image coordinates.

$$
x_{distorted} = A^{-1}(u,v))
$$

### 3 - Undistorted projected point to ray.
If we don't have distortion, computing $(\theta, \varphi)$ from $x_{undistorted}$ is relatively easy: 
- $\varphi$ is just the angle of the coordinate around the Z axis (roll)
- $\theta$ can be deduced by inverting $r(\theta)$ either numerically (we can numerically estimate an inverse function in the given range), or we can solve $\theta$ given $r(\theta)$ analytically.

### 2 - Deducing $x_{undistorted}$ from $x_{distorted}$ 
This is the hard part. Since we have the result of $x_{distorted} = F(\theta, \varphi) + S(\theta, \varphi)$ but we don't know how to deduce only the distortion part $S(\theta, \varphi) = \Delta_r(\theta, \varphi)u_r(\varphi) + \Delta_t(\theta, \varphi)u_{\varphi}(\varphi)$ 

We can describe the distortion part of a point $x_{undistorted}$ like so:
-  $S(\Phi) = S(F^{-1}(x_{undistorted}))$   