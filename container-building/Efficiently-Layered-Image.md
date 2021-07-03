---
parent: Minimize Image Inheritance
title: Efficiently Layered Image
---
# Efficiently Layered Image

To package an application for deployment in a container, you are designing an [application runtime image](Application-Runtime-Image.md). You already have a [minimal base image](minimal-base-image.md) that you've either downloaded or built yourself. You are writing a Dockerfile to install your application into the base image.

**How do you write a Dockerfile to build a container image with minimal complexity and maximum efficiency?**

[Application runtime image](Application-Runtime-Image.md) explains that an application image consists of three conceptual layers: OS libraries, language runtime, and application. The base image provides the first two of these conceptual layers, and hopefully you've chosen one that minimizes complexity and maximizes efficiency. Now your Dockerfile needs to not only deploy your application but also create an image that runs efficiently.

The efficiency of a container image is measured in multiple ways: How much bandwidth does it need to download? How much space does it consume in the [image registry](../container-architecture/image-registries-as-a-service.md)? How quickly does a new container start? How much memory do multiple containers from the same image consume when running in the same container engine? A container image built efficiently to work efficiently will optimize all of these measurements.

A container image appears to be monolithic, but is actually composed of layers. Each layer has a unique identifier and has a dependency on the layer before it. When you pull an image from one registry to another, the command pulls the top layer, which in turn pulls each successive layer used to build the complete image. For example, when we download the image for Ubuntu 14.04, we can see that consists of three layers. When the command is running, you can see the individual layers download concurrently and then extract in order. The completed download shows the three layers:

```shell
$ docker pull ubuntu:14.04
14.04: Pulling from library/ubuntu
2e6e20c8e2e6: Pull complete
0551a797c01d: Pull complete
512123a864da: Pull complete
Digest: sha256:5c01e896fa6eeaa41f3509c64af668d71d06e318cfe373dabab9d61b9eaf6441
Status: Downloaded newer image for ubuntu:14.04
docker.io/library/ubuntu:14.04
```

Different but related images share layers. For example, two images both built from `ubuntu:14.04` will share these first three layers. This way, when both images are downloaded and stored, the Ubuntu layers only need to be downloaded once and stored once. Compared to whichever image is downloaded first, the second image downloads faster and increases the size of the registry less because the Ubuntu layers were already downloaded and stored with the first image.

Running containers from the same image or related images also share layers. Whichever image is run first, the container engine has to load all of the layers for that image. Then to run the second container, the engine only has to load the layers that are different from the first container.

For two images to share a layer, not only must the layer's content be the same in both images, but the layer in both images must have the same predecessor layer. That predecessor layer must have the same predecessor, and so on. So two images can share a layer as long as it and all of its predecessors are the same.

Each command in a Dockerfile (e.g. `RUN`, `COPY`, `ADD`, etc.) creates a new layer in the resulting image. The fewer commands the Dockerfile needs to create the image, the fewer layers the image will have. If two images are the same size, the one with fewer layers will download faster and its containers will start faster.

Ideally, an image should have a low number of layers but those layers should be as reusable as possible. We see this in a [minimal base image](minimal-base-image.md) where the OS libraries composite layer, such as a version of Ubuntu, is very reusable; and the language runtime composite layer, such as a version of the Node.js runtime, is very reusable. The base image makes the combination of the two composite layers very reusable, and the small number of layers in each composite layer make the base image very efficient.

**Build an *efficiently layered image* that adds an optimized set of layers for the application to a base image with optimized layers.**

The question then is how to write the Dockerfile to deploy and configure the application in a low number of efficient layers.

A technique to make layers reusable is to move the commands that build layers that don't change to earlier in the Dockerfile. The layer for an application may not be reusable with other applications (the way the OS libraries and language runtime composite layers often are), but they can be reusable across multiple builds of the same application. For a new layer to be equivalent to one that has already been built, not only must it have the same contents, it also must have the same predecessors. Therefore, move the commands with data that's relatively static to the beginning of the Dockerfile and similarly move commands with data that changes frequently to the end of the Dockerfile. The earlier layers will be more reusable because their data doesn't change and because the layers before them don't change.

A technique to create fewer layers is to combine multiple actions into a single Docker command. Because each command creates a new layer, fewer commands that perform the same actions will create fewer layers.

A technique to make layers smaller, and therefore make the complete image smaller, is to only load the files and data that are needed. It may be convenient to load all of the files that are in an external directory, but the image will be smaller if it only loads the external files it will actually use.

In addition to these techniques to optimize lines of code in a Dockerfile, you should also optimize the build process using a [multistage image build](multistage-image-build.md). Once you have built your *efficiently layered image*, store it in an [image registry](../container-architecture/image-registries-as-a-service.md).

## Example

An unoptimized Dockerfile builds images that are bigger than they need to be, with more layers than are required, and layers that are difficult to reuse. An example of an unoptimized Dockerfile might be:

```dockerfile
FROM ubuntu:14.04
COPY . /app
RUN apt-get update
RUN apt-get install -y openjdk-8-jre
RUN apt-get clean
CMD [“java”, “-jar”, “/app/sample.jar”]
```

Let's optimize this file.

Technique 1: Move layers that don't change to the top of the file.

The Ubuntu packages being installed will not change very often, whereas the app being installed will change whenever it is rebuilt with new code for a bug fix or a new feature. Therefore, put the `apt-get` commands to install the Ubuntu packages before the `COPY` command to load the application:

```dockerfile
FROM ubuntu:14.04
RUN apt-get update
RUN apt-get install -y openjdk-8-jre
RUN apt-get clean
COPY . /app
CMD [“java”, “-jar”, “/app/sample.jar”]
```

Technique 2: Combine multiple actions into a single Docker command.

The three `apt-get` commands can be combined into a single `RUN` command:

```dockerfile
FROM ubuntu:14.04
RUN apt-get update && \
    apt-get install -y openjdk-8-jre && \
    apt-get clean
COPY . /app
CMD [“java”, “-jar”, “/app/sample.jar”]
```

Technique 3: Only load the files and data that are needed.

The `COPY` command loads all files from the local directory into the image even though the image never uses most of them. Therefore, only load the file that the image uses:

```dockerfile
FROM ubuntu:14.04
RUN apt-get update && \
    apt-get install -y openjdk-8-jre && \
    apt-get clean
COPY sample.jar /app
CMD [“java”, “-jar”, “/app/sample.jar”]
```

