### Camera Parameters
- $fov_y$ - field of view in the vertical axis
- aspect - $\frac {fov_x} {fov_y}$ , this is the aspect ratio of the camera image.
- z_near, z_far - these determine how to map z coordinates into the interval $[0, 1]

### Matrix Form
- $\alpha = \frac {fov_y} {2}$ 

$$
\begin{pmatrix}
\frac {1} {aspect \cdot tan(\alpha)} && 0 && 0 && 0 \\
0 && \frac {1} { tan(\alpha)} && 0 && 0 \\
0 && 0 && \frac {-(z_{far} + z_{near})} {z_{far} - z_{near}} && \frac {-2(z_{far} \cdot z_{near})} {z_{far} - z_{near}} \\
0 && 0 && -1 && 0 \\
\end{pmatrix}
$$


### Assumptions
- the pinhole camera is looking at the $-z$ direction
- the imager span the range $[-1, 1]$ in both $x$ and $y$ direction
- the field of view in $x$ is $apsect \cdot fov_y$ 

### Analysis
1. The focal length is the z-distance of the imager from the origin. and the imager spans $[-1,1]$ in the vertical direction.
   so if we take a ray $r_y$ that goes on the edge of the vertical field of view we can calulate its projection on the $y$ axis: 
   $\frac {y'} {f} = \frac 1  {f} = tan(fov_y / 2) \rightarrow f=\frac 1 {tan(fov_y / 2)}$
2. On the horizontal axis, our imager spans $[-aspect, aspect]$, so if we take a ray $r_x$ and that goes on the edge of the vertical field of view:
   $\frac {x'} f = \frac {aspect} f = \frac {apsect} {tan(fov_y / 2)}$ 
- the image plane has a span of $[-1, 1]$ in both $x$ and $y$ axis
- the image plane is located at distance $tan(fov_y / 2)$ 

- if you think of a standard pinhole camera, then the image plane has a dimention of 