---
parent: Container Building
title: Intentional Layer
---
# Intentional Layer

You are building a container image and have a complex Dockerfile.

**How do you make sure that you haven’t made your docker containers excessively large and complex by adding too many layers?**

A Layer is a change to an image, or an intermediate image. Docker is built on the Union file system which allows you to transparently merge together many different filesystems (or branches) into a single coherent filesystem. Certain commands in a docker file (RUN, COPY, ADD) create a new layer. . Other instructions create temporary intermediate images, and do not increase the size of the build.  Essentially, each layer is its own branch.  However, this also ties into the concept of building docker image - if you make a change to a docker file, only those layers that are put down after the change are rebuilt. 

**Only create permanent layers intentionally.  Think carefully about how many layers you are creating and reduce the number of total layers.**

Especially when using the RUN command, combine Linux commands together as much as possible (within reason) to reduce image size.  While this is not the only reason for combining Linux commands together inside a RUN, this is a good one.  
