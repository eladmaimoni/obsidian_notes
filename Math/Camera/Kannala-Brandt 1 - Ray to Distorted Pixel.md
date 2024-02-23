# Ray to Distorted Pixel  $A(F(\theta, \varphi) + D(\theta, \varphi))$

### Object ray to projected point on the virtual image plane (undistorted)

$$
x_{projected-undistorted} = F(\theta,\varphi) = r(\theta)u_r(\varphi)
$$
### Projected point to distorted projected point
$$
x_{distorted} = x_{projected-undistorted}  + \Delta_r(\theta, \varphi)u_r(\varphi) + \Delta_t(\theta, \varphi)u_{\varphi}(\varphi)
$$
### Distorted projected point to pixel $(u,v)$
$$
  \begin{pmatrix}
  u \\
  v
  \end{pmatrix}
  =
  A(x_{distorted})
  =
    \begin{pmatrix}
  m_u && 0 \\
  0 && m_v
  \end{pmatrix}x_{distorted}
  +
 \begin{pmatrix}
  u_0 \\
  v_0
  \end{pmatrix}
$$
### Terms breakdown
- $\theta$ - in camera space, the object angle relative to the principle axis (Z axis)
- $\varphi$ - in camera space, the object angle relative to the x axis (roll, righthand rule with Z axis).
	  Note: $\varphi$ is the same for both camera space and projected image space (undistorted)
- $u_r(\varphi)$ - a unit vector in the radial direction in the undistorted image. This is the projection onto the $x$ and $y$ axis in the undistorted image:
  $$
  u_r({\varphi}) = \begin{pmatrix}
  \cos(\varphi) \\
  \sin(\varphi)
  \end{pmatrix}
 $$
- $u_t(\varphi)$ - a unit vector in the tangential direction in the undistorted image.
    $$
  u_t({\varphi}) = \begin{pmatrix}
  -\sin(\varphi) \\
  \cos(\varphi)
  \end{pmatrix}
 $$
 - $r(\theta)$ - this is the derived lens projection model. In pinhole this would simply be $f\tan(\theta)$ that determines the pixel location on the image.
$$
r(\theta) = k_1 \theta + k_2\theta^3 + k_3\theta^5 + k_4\theta^7 + k_5\theta^9
$$   Notes: 
	 - this part does not account for distortion, it is simply aimed to model the actual projection occurring in a wide angle camera when an object is at angle $(\theta, \varphi)$ from the principal point / axis

- $\Delta_r(\theta, \varphi)u_r(\varphi)$ - radial distortion. this is an additive term that model the lens distortion in the radial direction $u_r$ as a function of  $(\theta, \varphi)$
$$
\Delta_r(\theta, \varphi)=(l_1\theta + l_2\theta^3 + l_3\theta^5)(i_1
\cos(\varphi) + i_2\sin(\varphi) + i_3\cos(2\varphi) + i_4\sin(2\varphi))
$$
-  $\Delta_t(\theta, \varphi)u_t(\varphi)$ - tangential distortion. this is an additive term that model the lens distortion in the tangential direction $u_t$ as a function of  $(\theta, \varphi)$
$$
\Delta_t(\theta, \varphi)=(m_1\theta + m_2\theta^3 + m_3\theta^5)(j_1
\cos(\varphi) + j_2\sin(\varphi) + j_3\cos(2\varphi) + j_4\sin(2\varphi))
$$

