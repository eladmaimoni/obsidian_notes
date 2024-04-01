
### Requirements
- a complex object such as a MainCrane contains a lot of components
- some of them are cameras that move with the crane elements
- the scene (or parts of it) can be rendered from these views

### Developer flow
- When a crane is constructed it constructs its parts (entities)
- Each part may contain different components (transform, collision, render etc)
- Ideally there will be no coupling between the scene rendering logic (draws) to the component management.
- So for instance, when we add a camera object (not component) that is part of a crane it will have the different components:
  - RigidTransformComponent (scene graph)
  - PerspectiveTransformComponent
  - UniformBufferComponent
- The components will only contain data and buffers that needs to be updated when the scene updates
	- scene graph updates transformations
	- render scene updates the uniform buffers for transformed objects
### Problem
- when we wish to add a render object that contains constant buffers (uniforms), it is typically associated with a specific descriptor set layout. 
- we don't need the descriptor set layout to create the constant buffer. however:
- we need access to the descriptor set layout in order to upd

### Ideas
1. make sure your shaders have the save descriptor set layout, that contain all the possible binding points. 
2. when allocating a descriptor set, as long as it is allocated with a compatible layout, it should be alright.
3. cache all pipeline layout by id (or combinations of ids). when you need to allocate a descriptor set, ask the cache to provide you with the descriptor set layout for that id.
   - not that clean, since when we want to allocate a camera buffer, we specifically mention which shader we wish this to use.
   - not that terrible, we avoid the coupling between object creation and rendering it (but we have a fragile point where the descriptor set for the view pass must match)
1. 