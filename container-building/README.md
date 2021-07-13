---
title: Container Building
nav_order : 14
has_children: true
---
# Image Building Patterns

In other parts of this work we have discussed the advantages of containers as a technology for building applications to be deployed into a Hybrid Cloud Environment.  We have also introduced the concept of Container Orchestration projects like Kubernetes and their prevalence as a part of the Cloud ecosystem.  Finally, we've covered specialized issues involved in building DevOps Pipelines for applications that are to be delivered as Docker (or other container technology) Images.  In this section, we will adddress another fundamental set of problems in developing container-based applications; that is building these images and following best practices for image development. 

These patterns are important because, like nearly any other technology, it's easy to get lost along the way of adopting container images and end up not gaining the benefits that the technology promises.  In particular, as we have discussed earlier, teams adopt container technology because it promises:

1. Smaller memory footprints for applications (because of all the sharing that happens in the container model as opposed to a VM Model), resulting in denser packing of applications into the same hardware
2. Faster application startup (again, because of the shared operating system, container startup is faster than VM startup)
3. Better isolation and security than in a model where multiple standard processes share a common VM

Unfortunately, these benefits do not come for free.  You can easily end up with very large container images that contain unnecessary elements that can bloat your resulting containers. Likewise, it's possible to add unnecessary process startup and other resource requirements that can slow down your image startup from milliseconds to seconds or minutes.  And finally, it's not just possible but far to easy to render the promised security benefits moot and allow malware or simply badly coded applications to escalate privileges and gain improper access to the resources of the container host.

We cannot solve every possible problem that can lead to this loss of benefits, but there are several common approaches that can help to guarantee that your images will remain small, fast and secure.  The patterns that capture those approaches are:

+ [Application Runtime Image](Application-Runtime-Image.md) is the place to begin in that it shows how to build most application images from a few basic images without letting container inheritance get out of hand.
+ [Minimal Base Image](minimal-base-image.md) builds on this basic principle by ensuring that you think about what your image is based upon before starting development
+ [Efficiently Layered Image](Efficiently-Layered-Image.md) deals with the basic question of how many literal layers your final application image should contain and how to minimize your layer depth and memory footprint.
+ [Least Privilege](least-privilege.md) addresses how to secure your container image by not granting unneeded permissions to resources
+ [Multistage Build](multistage-image-build.md) discusses how the process of constructing the artifacts in an image can be separated from the final image for production
+ [Visualize Image Dependencies](Visualize-Image-Dependencies.md) reinforces the importance of visualizing the set of dependencies of different types among images to track the possible impact of changes within the set of images

