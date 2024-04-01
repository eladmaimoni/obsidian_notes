
# Background
- When we  allocate a descriptor set for a set of buffers, we must know the descriptor set layout
- when we bind the descriptor set, we must provide the pipeline layout
- a pipeline is constructed with a descriptor set layout and a pipeline layout
- In a lot of cases, multiple pipelines share a subset of constant (uniform) buffers. for example per view uniform buffers.
- For example a "View" that defines the "per view descriptor set" and has a bunch of pipelines associated with it.

# Problem
 - What we wish to do in the allocation phase is
```
class PerViewObject
{
	PerViewObject(...)
	{
		AllocateBuffersAndDescriptorSetForThisView();
		// but how do we obtain the right descriptor set layout
		// without coupling the PerViewObject with all the pipelines in this view?
	}
}
```

  - what we would like to do iin the drawing phase is:
```
for (view in views)
{
	BindPerViewDescriptorSet();
	// but how can we make sure the pipelines are compatible?
	// how can we reduce coupling between the view and the pipelines?
	for (pipeline in pipelines)
	{
		BindPipelineSpeceificDescriptorSet()
		DrawAllObjectsAssociatedWithThePipelines();
	}
}  
```

