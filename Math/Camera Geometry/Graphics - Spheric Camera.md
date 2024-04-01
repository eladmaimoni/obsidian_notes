
1. we have a virtual camera that has a standard camera transform
2. in the vertex / geometry shader, we map input vertices to this camera space
3. so all geometry / lighting is done in this space.
4. for pixel projection, we need to account for spheric params and ROI.
   
Pixel Projection
- The ROI calculation gives us 2 additional parameters:
  - rotation matrix. this matrix is applied to vertices (rays) in camera space and maps it to the "roi rotated camera" space.
  - radians per spheric pixel - this is used to map pixels into rays.
    we need to map rays to pixels. so we need the inverse factor:
    

- rotation matrix. this matrix is applied to vertices (rays) in the camera