Title: Container Dependency Model

Context:

You have a medium to large estate of container images where each image is dependent on multiple images.

Problem:

The underlying layering mechanism that containers use are meaning it's difficult to see how an individual image is made up of the various base images within the estate.  In addition it's hard to see all the images that utilize the core base images.

Forces:

* You need to understand which images in the estate are orphaned post version upgrades
* You need to understand all of the images that are affected by patching an image
* You need to understand which third party images are used or unused
* You need a simple overview of all images in the estate
* Licensing and auditing compliance

Results:

You should use a tool that can generate a container dependency model.   The tool should be able to inspect all docker images in your container registry and generate a model that shows the metadata and the dependencies of the image from the dockerfile.

Results:

A container dependency model will allow you to see:

* Every image in your estate
* The version of the image
* The registry that the image resides in \(and whether it's public or private\)
* All images the image is dependent on

The following diagram shows an example container dependency model.



![](/assets/container_dependency_model.png)

