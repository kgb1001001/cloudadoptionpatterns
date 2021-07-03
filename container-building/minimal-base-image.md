---
parent: Minimize Image Inheritance
title: Minimal Base Image
---
# Minimal Base Image

To package an application for deployment in a container, you are designing an [application runtime image](Application-Runtime-Image.md). You want to be able to take advantage of the benefits of containers, such as rapid startup and small memory footprint. However, you want to spend your time developing your application and not spending time and effort in packaging.

**How do you ensure that you reduce the total amount of work you have to do in preparing your container images while ensuring that the image includes the latest patches and a minimal attack surface?**

*Application runtime image* explains that an application image consists of three composite layers: OS libraries, language runtime, and application. Where do the first two layers come from?

Every container image is built from a more basic container image. (Makes you wonder where the first image came from!) What base image should you build your image from? Clearly, one that contains the OS libraries and, ideally, the language runtime needed to run your application.

The community has lots of base images to choose from. They're available in widely-shared [image registries](../container-architecture/image-registries-as-a-service.md) such as Docker Hub and Red Hat's registry of certified container images.

The problem with using someone else's image is that you need to be able to trust it and the organization who built it. The image needs to have been built well, with no extraneous software that bloats the image and introduces new points for hackers to attack, and that doesn't include any malicious software.

Your application won't run in a base image that only contains a few base OS libraries. Your application is written in a *modern application language* and requires that language runtime. So either you will need to install that runtime into a base image that you choose, or better yet, choose a base image that includes the runtime that your application requires. 

**Select a *minimal base image* that includes only the OS libraries needed for your application's language runtime, and ideally one that already includes the language runtime as well.**

Deploying your application into such a base image will be fairly easy. If the base image does not include the language runtime for your application, install it. Once it's installed, or if the base image already includes the the language runtime, deploy your application into that image and save it as the image for your application.

A base image designed to include a specific language runtime can be better optimized because it's designed to only include the OS libraries that the runtime requires and those libraries can be configured for that particular language runtime.

How do you know which base images you can trust and, better yet, how they were built? Docker Hub has a designation called Official Images, ones that Docker, Inc. has reviewed and published. For example, the images in the `ubuntu`, `alpine`, `node`, and `openjdk` directories (and many more) on Docker Hub are all labeled as "Docker Official Images."

Another option for finding trusted images is to look on the software vendor's website. Often they have instructions for downloading their official images, such as specifying their official directory in Docker Hub. For example, the Open Liberty website says to pull the open-liberty image, which pulls from the `open-liberty` directory on Docker Hub. The images in this directory are Docker Official Images which, as the Docker Hub website describes, are maintained by the Open Liberty Community.

Some vendors offer prebuilt base images for a range of uses. For example, Red Hat offers a set of Universal Base Images (UBI) that contain libraries from Red Hat Enterprise Linux (RHEL) and optionally a language runtime for languages like Java (OpenJDK), Node.js, Python, PHP, and others.

Registries such as Docker Hub often show how the image is built. You can review these to confirm that an image is built properly before trusting it. For example, the `OpenLiberty/ci.docker` repository in GitHub shows releases of the Open Liberty container image and the Dockerfiles used to build them. Likewise, Red Hat's registry of certified container images shows how each UBI is built, its health rating, and more.

Many base images have multiple builds of the same software version. To save space in the final container image, use the smallest build that the application can run in successfully.

Once you have a base image that will run your application, use it to build an [efficiently layered image](intentional-layer.md) that includes the application.

## Example: Java SE from AdoptOpenJDK

AdoptOpenJDK is a community that produces free OpenJDK (Java) binaries. Their `AdoptOpenJDK/openjdk-docker` repository in GitHub contains the source code they use to build the images they push to the `adoptopenjdk` directory in Docker Hub as Docker Official Images. Their Dockerfiles show that they install their JDK on Ubuntu images, which are also Official Images in Docker Hub.

We asked earlier: Where did the first container image come from? The Ubuntu image shows how that's done now. Its Dockerfiles build its images from a base image called `scratch`. Docker's documentation explains:

> You can use Docker’s reserved, minimal image, `scratch`, as a starting point for building containers.
>
> While `scratch` appears in Docker’s repository on the hub, you can’t pull it, run it, or tag any image with the name `scratch`.

To build an image for a Java SE application, start your Dockerfile with a line like this:

```dockerfile
FROM adoptopenjdk:8-jre-openj9
```

## Example: Jakarta EE from Open Liberty

Open Liberty is an open source application server that implements the Java EE and Jakarta EE APIs, based on IBM's WebSphere Liberty. Their `OpenLiberty/ci.docker` repository in GitHub contains the Dockerfiles they use to build the images they push to the `open-liberty` directory in Docker Hub as Docker Official Images. Their Dockerfiles show that they build their images from AdoptOpenJDK images (explained above).

To build an image for a Jakarta EE application, start your Dockerfile with a line like this:

```dockerfile
FROM open-liberty:full-java11-openj9
```

However, most applications don't need the full Liberty build to run properly. Choose the smallest build that the application can run in.

For example, the `kernel-slim-java11-openj9` build of Open Liberty is smaller than the `full-java11-openj9` build:

| build | architecture | size |
| ----- | ----- | ----- |
| full-java11-openj9 | linux/amd64 | 277.35 MB |
| kernel-slim-java11-openj9 | linux/amd64 | 102.61 MB |

The full build is 2.7 times larger than the slim build.

The catch is that the slim builds don't include any Liberty features, just the Liberty kernel. The full builds include all of the features, so of course they are larger.

Few applications require all of the Liberty features. A approach that creates a more optimized runtime is to start with the kernel and load just the features that the application requires. The application specifies those features in its server configuration, the `server.xml` file. To use this technique to build a container image for an application running in Liberty, put commands like these in the Dockerfile:

```dockerfile
## Start from a kernel-slim build that doesn't have any features loaded
FROM open-liberty:kernel-slim-java8-openj9

# Add a Liberty server configuration that specifies the features the application requires
COPY --chown=1001:0  server.xml /config/

. . .

# This script will apply the server configurations, thereby loading the features it specifies
RUN configure.sh
```

These Dockerfile commands result in an image that is as small as possible because it only includes the Liberty features that the application requires (as specified in `server.xml`).

## Example: Node.js from Red Hat as a Universal Base Image

Red Hat Universal Base Images (UBI) are images that Red Hat supports when running in Red Hat OpenShift and that are freely distributable. Red Hat makes available UBIs for several language runtimes and versions. Their certified container images registry shows the Dockerfiles they use to build their UBIs. They build from the UBI 8 images OpenShift uses for its source-to-image (s2i) feature, which the registry shows is built from their base UBI image, which is built on the Koji image from the Fedora project.

To build an image based on a UBI for a Node.js 14 application, start your Dockerfile with a line like this:

```dockerfile
FROM registry.access.redhat.com/ubi8/nodejs-14:latest
```

