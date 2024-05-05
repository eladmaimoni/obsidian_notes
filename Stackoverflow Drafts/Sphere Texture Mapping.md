I am trying to render my 3d scene using a spherical projection model. sort of like the method described [here][1]:

> The rendering is done in two steps: first a cube map is filled with six renderings for the six directions defined by the cube, then this cube map is applied as a texture on a 3D model representing the mapping of the dome, which is captured and renderer by another camera.

In my vulkan renderer, I render a 3d scene to a cube map. Each cube face represents a 90x90 degrees fov of my scene. After examining the cube map in renderdoc, it seems the scene is rendered correctly:

 - +X cube face shows the view to the right of my camera
 - -X cube face shows the view to the left of my camera 
 - +Y cube face shows the view below of my camera
 - -Y cube face shows the view above of my camera 
 - +Z cube face shows the view in front of my camera
 - -Z cube face shows the view behind my camera

Once the cube map is created, I wish to sample it in a separate pass.
In this pass, I assume I have my camera set at the center of the cube, looking towards the Z axis.
The camera is a spherical camera, so this means that each pixel directly maps to sphere viewing angles using a fixed ratio:


  [1]: https://emmanueldurand.net/spherical_projection/