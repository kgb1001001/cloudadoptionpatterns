---
parent: Minimize Image Inheritence
title: Minimal Base Image
---
# Minimal Base Image

To package an application for deployment in a container, you are designing an [application runtime image](Minimize-Image-Inheritence.md). You want to be able to take advantage of the benefits of containers, such as rapid startup and small memory footprint. However, you want to spend your time developing your application and not spending time and effort in packaging.

**How do you ensure that you reduce the total amount of work you have to do in preparing your container images while ensuring that the image includes the latest patches and a minimal attack surface?**

Every container image is built from a more basic container image. (Makes you wonder where the first image came from!) What base image should you build your image from?

The community has lots of base images to choose from. They're available in widely-shared [image registries](../container-architecture/image-registries-as-a-service.md) such as Docker Hub and Red Hat's registry of certified container images.

The problem with using someone else's image is that you need to be able to trust it and the organization who built it. The image needs to have been built well, with no extranious sofware that bloats the image and introduces new points for hackers to attack, and that doesn't include any malicious software.

Your application won't run in a base image that only contains a few base OS libraries. Your application is written in a *modern application language* and requires that language runtime. So either you will need to install that runtime into a base image that you choose, or better yet, choose a base image that includes the runtime that your application requires. 

**Select a *minimal base image* that includes only the OS libraries needed for your application's language runtime, and ideally one that already includes the language runtime as well.**

Deploying your application into such a base image will be fairly easy. If the base image does not include the language runtime for your application, install it. Once it's installed, or if the base image already includes the the language runtime, deploy your application into that image and save it as the image for your application.

A base image designed to include a specific language runtime can be better optimized because it's designed to only include the OS libraries that the runtime requires and those libraries can be configured for that particular language runtime.

How do you know which base images you can trust and, better yet, how they were built? Docker Hub has a designation called Official Images, ones that Docker, Inc. has reviewed and published. For example, the images in the *ubuntu*, *alpine*, *node*, and *openjdk* directories (and many more) on Docker Hub are all labeled as "Docker Official Images."

Another option for finding trusted images is to look on the software vendor's website. Often they have instructions for downloading their official images, such as specifying their official directory in Docker Hub. For example, the Open Liberty website says to pull the open-liberty image, which pulls from the *open-liberty* directory on Docker Hub. The images in this directory are Docker Official Images which, as the Docker Hub website describes, are maintained by the Open Liberty Community.

Some vendors offer prebuilt base images for a range of uses. For example, Red Hat offers a set of Universal Base Images (UBI) that contain libraries from Red Hat Enterprise Linux (RHEL) and optionally a language runtime for languages like Java (OpenJDK), Node.js, Python, PHP, and others.

Resistries such as Docker Hub often show how the image is built. You can review these to confirm that an image is built properly before trusting it. For example, the OpenLiberty/ci.docker repository in GitHub shows releases of the Open Liberty container image and the Dockerfiles used to build them. Likewise, Red Hat's registry of certified container images shows how each UBI is built, its health rating, and more.

## Example: AdoptOpenJDK

AdoptOpenJDK is a community that produces free OpenJDK (Java) binaries. Their AdoptOpenJDK/openjdk-docker repositry in GitHub contains the source code they use to build the images they push to the *adoptopenjdk* directory in Docker Hub as Docker Official Images. To build an image for a Java SE application, start your Dockerfile with a line like this:

```dockerfile
FROM adoptopenjdk:8-jre-openj9
```

## Example: Red Hat Universal Base Image for Node.js 14

Red Hat Universal Base Images (UBI) are images that Red Hat supports when running in Red Hat OpenShift and that are freely distributable. Red Hat makes available UBIs for several language runtimes and versions. To build an image for a Node.js 14 applicaion, start your Dockerfile with a line like this:

```dockerfile
FROM registry.access.redhat.com/ubi8/nodejs-14:latest
```


