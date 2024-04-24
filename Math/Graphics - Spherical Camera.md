
- $fov_x$ -  field of view in the horizontal dimension
- if we have our angle (azimuth / elevation) we can obtain the NDC coordinate by 
  $$x_{NDC} = \frac {\theta_x}{fov_x}$$
  $$y_{NDC} = \frac {\theta_y}{fov_y}$$
  

$$
\begin{pmatrix}
\frac {1} {fov_x} && 0 && 0 && 0 \\
0 && \frac {1} { fov_y} && 0 && 0 \\
0 && 0 && \frac {z_{far}} {z_{far} - z_{near}} && - \frac {z_{far}z_{near}} {z_{far} - z_{near}}\\
0 && 0 && 1 && 0 \\
\end{pmatrix}
\begin{pmatrix}
\theta_x \cdot z \\
\theta_y \cdot z \\
z \\
1
\end{pmatrix}
$$