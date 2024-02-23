### Problem Setup
- 2 coordinate systems that are related to each other with a rotation: 
$$w = R * v$$
- Set of corresponding 3D vectors (that describe the same point / direction)
### Example
- we have 2 images taken from a known camera model(s). we can deduce matching 3d vectors from matching 2d points. from the set of matching vectors we can deduce the rotation $R$ between the 2 cameras.

### Math

Goal: Find the minimum of 
$$
\sum_{k=1}^Na_k{w_k - Rv_k}  
$$
