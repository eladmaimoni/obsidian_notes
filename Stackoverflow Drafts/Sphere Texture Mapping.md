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
In this pass, I assume I have my spheric 'camera' set at the center of the cube, looking towards the Z axis, and projects the scene into a 1080x640 image.
Since the camera is a spherical camera, it means that each pixel directly maps to sphere viewing angles using a fixed ratio `spheric_radians_per_pixel`.
```
float3 convert_azimuth_elevation_to_dir(float azimuth, float inverse_elevation)
{
    // assuming the vulkan camera is looking to +Z, +Y is down, +X is right
    // elevation is the angle between the vector and its projection on the XZ plane.
    // elevation is usually positive when the angle points upwards, towards the (-Y) direction
    // so inverse direction is used here, it is positive when the angle points downwards, towards the (+Y) direction
    // azimuth is the angle between the XZ projection and the Z axis, positive when the angle is pointing rightward (+X) 
    float3 vector_out;
    float xz_plane_projection_cos = cos(inverse_elevation); // always positive
    float xz_plane_projection_sin = sin(inverse_elevation);
    float yz_plane_projection_cos = cos(azimuth);
    float yz_plane_projection_sin = sin(azimuth);
    
    vector_out.x = xz_plane_projection_cos * yz_plane_projection_sin;
    vector_out.y = xz_plane_projection_sin;
    vector_out.z = xz_plane_projection_cos * yz_plane_projection_cos;
    return vector_out;
}


[numthreads(16, 16, 1)]
void compute_main(uint3 dispatchThreadID : SV_DispatchThreadID)
{
    const float radians_per_pixel = spheric_radians_per_pixel.x;
    int2 tex_coord = dispatchThreadID.xy;
    float coord_x = (float)tex_coord.x - (1080.0f / 2.0f);
    float coord_y = (float)tex_coord.y - (640.0f / 2.0f);
    float azimuth = coord_x * radians_per_pixel;
    float inverse_elevation = coord_y * radians_per_pixel;

	float3 direction = convert_azimuth_elevation_to_dir(azimuth, inverse_elevation);
	float4 color = cubemapTexture.SampleLevel(cubemapSampler, direction, 0.0);
	outputTexture[tex_coord] = float4(color, 1.0f);
}

```

It seems that the code manages to sample the expected cube plane at each direction of the image (added image here for reference - light green is +Y, dark green is -Y,  light red +X, dark red -X. blueish is +Z).
However, it seems that the each cube texture plane is sampled incorrectly in terms of uv: I managed to hack around it using this piece of code:
```
   if (abs(direction.z) > abs(direction.x) && abs(direction.z) > abs(direction.y))
   {
       direction.y = -direction.y;
   }
   if (abs(direction.y) > abs(direction.x) && abs(direction.y) > abs(direction.z))
   {
       direction.z = -direction.z;
   }
   if (abs(direction.x) > abs(direction.y) && abs(direction.x) > abs(direction.z))
   {
       direction.y = -direction.y;
   }
```

I suspect the hack might be related to the fact that I am using a compute shader to sample the cubmap, and not rendering a 3D cube with the cubemap textured onto it.

So how to correctly sample a compute 











  [1]: https://emmanueldurand.net/spherical_projection/