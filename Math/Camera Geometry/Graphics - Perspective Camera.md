### Camera Parameters
- $fov_y$ - field of view in the vertical axis
- aspect - $\frac {fov_x} {fov_y}$ , this is the aspect ratio of the camera image.
- z_near, z_far - these determine how to map z coordinates into the interval $[0, 1]

### Assumptions
- the pinhole camera is looking at the $-z$ direction
- the imager span the range $[-1, 1]$ in $y$ direction
- to deduce the focal length: $\frac 1 f = tan(0.5 \cdot fov_y) \rightarrow f = \frac 1 {tan(0.5 \cdot fov_y)}$ 
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

- Result after multiplication and divide by $w$:
	$x' = \frac 1 {aspect} \cdot (f \cdot \frac y {-z})$ 
	$y' = f \cdot \frac x {-z}$ 
	
### Matrix Analysis
1. the NDC coordinate $y'$ coordinate is deduced using standard pinhole formula $y' = f \cdot \frac y {|z|}$.
2. The NDC coordinate for $x'$ is deduced similarly (the focal length is the same), however, since the imager in the $x$ dimension is larger by a factor of $aspect$, we divide the result by $apsect$ so that to 'shrink' the range $[-aspect, aspect]$ to $[-1, 1]$. effectively creating a larger imager in that axis.
   
3. the Z axis goes through a different manipulation. we need to remember that the $z$ axis is not drawn. the sole purpose of the manipulation is for writing into the depth buffer.
- the image plane has a span of $[-1, 1]$ in both $x$ and $y$ axis
- the image plane is located at distance $tan(fov_y / 2)$ 

- if you think of a standard pinhole camera, then the image plane has a dimention of 