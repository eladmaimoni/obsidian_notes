CubeRenderCamera 
2. will create 6 transform components for all 6 views, one of them will be "primary" - the forward looking one that is the parent of all the rest
3. will create 1 RenderCubeViewProjectionUniformBufferComponent to hold the view transform uniform (6 transformations)
4. RenderCubeViewProjectionUniformBufferComponent will hold 


Questions:
1. What is the order of the cube map rendering ? what determines the face index we get in the render shader

1. **Positive X (Right)**
2. **Negative X (Left)**
3. **Positive Y (Top)**
4. **Negative Y (Bottom)**
5. **Positive Z (Front)**
6. **Negative Z (Back)**

Alternative approach:
1. use the standard view block in hlsl - only one camera matrix.
2. per view - we know the additional rotation matrix we need to write down
3. declare the matrices in an array inside the shader - per view!
   this is simple.





