---
parent: Minimize Image Inheritence
title: Minimal Base Image
---
# Minimal Base Image

To package an application for deployment in a container, you are designing an [application runtime image](Minimize-Image-Inheritence.md). You want to be able to take advantage of the benefits of containers, such as rapid startup and small memory footprint. However, you want to spend your time developing your application and not spending time and effort in packaging.

**How do you ensure that you reduce the total amount of work you have to do in preparing your container images while ensuring that the image includes the latest patches and a minimal attack surface?**

Every container image is built from a more basic container image. (Makes you wonder where the first image came from!) What base image should you build your image from?

The community has lots of base images to choose from. They're available in widely-shared [image registries](../container-architecture/image-registries-as-a-service.md) such as Docker Hub.

The problem with using someone else's image is that you need to be able to trust them. The image needs to have been built well, with no extranious sofware that bloats the image and introduces new points for hackers to attack, and that doesn't include any malicious software.

Your application won't run in a base image that only contains a few base Linux libraries. Your application is written in a *modern application language* and requires that language runtime. So either you will need to install that runtime into a base image that you choose, or better yet, choose a base image that includes the runtime that your application requires. 

**Select a *minimal base image* that includes only the Linux libraries needed for your application's language runtime, and ideally one that already includes the language runtime as well.**

Deploying your application into such a base image will be fairly easy. If the base image does not include the language runtime for your application, install it. Once it's installed, or if the base image already includes the the language runtime, deploy your application into that image and save it as the image for your application.

How do you know which base images you can trust and, better yet, how they were built? Docker Hub has a designation called Official Images, ones that Docker, Inc. has reviewed and published. For example, the images in the *ubuntu*, *alpine*, *node*, and *openjdk* directories on Docker Hub are all labeled as "Docker Official Images."

A base image designed to include a specific language runtime can be better optimized because it's designed to only include the Linux libraries that the runtime requires and those libraries can be configured for that particular language runtime.