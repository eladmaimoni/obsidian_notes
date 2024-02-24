Assuming no distortion, we would like to estimate the projection model:
$$
x_{undistorted} = (k_1 \theta + k_2\theta^3 + k_3\theta^5 + k_4\theta^7 + k_5\theta^9)
\begin{pmatrix}
  \cos(\varphi) \\
  \sin(\varphi)
  \end{pmatrix}
$$
We have $N$ observations in the form of $pixel \rightarrow (azimuth, elevation)$:

1. transform each pixel observation into normalized coordinates by using $A^{-1}$ 
2. compute $r$ for each normalized pixel observation
3. compute $\theta$ for each pair of $(azimuth, elevation)$
4. we can now estimate this using LS:
$$
\begin{pmatrix}
\theta_1 && \theta_1^3 && \theta_1^5 && \theta_1^7 && \theta_1^7  \\
\theta_2 && \theta_2^3 && \theta_2^5 && \theta_2^7 && \theta_2^7  \\
\theta_3 && \theta_3^3 && \theta_3^5 && \theta_3^7 && \theta_3^7  \\
\vdots && \vdots &&\vdots && \vdots && \vdots \\
\theta_N && \theta_N^3 && \theta_N^5 && \theta_N^7 && \theta_N^7  \\
\end{pmatrix}

\begin{pmatrix}
k_1 \\
k_2 \\
k_3 \\
k_4 \\
k_5 \\
\end{pmatrix}
=
\begin{pmatrix}
r_1 \\
r_2 \\
r_3 \\
\vdots \\
r_N \\
\end{pmatrix}
$$
For the **inverse transformation**, my best idea is to estimate it in the range $[0, \theta_{max}]$ by using the same form polynomial (since this is an odd function) . we can do the exact same LS only swap the roles of $\theta$ and $r$.