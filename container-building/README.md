---
title: Container Building
nav_order : 14
has_children: true
---
# Image Building Patterns

This chapter is a work in progress as we are documenting patterns around the process of building images and best practices for image development. These patterns include:

+ [Minimal Base Image](minimal-base-image.md) talks about how you need to think about what your image is based upon before starting development
+ [Intentional Layer](intentional-layer.md) deals with the basic question of how many layers your image should contain
+ [Least Privilege](least-privilege.md) addresses how to secure your container image
+ [Multistage Build](multistage-image-build.md) discusses how the process of constructing the artifacts in an image can be separated from the final image for production
+ [Minimize Image Inheritance](Minimize-Image-Inheritance.md) deals with the issue that container inheritance can easily get out of hand.
+ [Visualize Container Dependencies](container-dependency-model.md) reinforces the importance of visualizing the set of dependencies of different types among images 

