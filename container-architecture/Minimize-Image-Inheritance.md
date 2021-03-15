# Minimize Image Inheritance

You are practicing Container DevOps and building many Docker images.

**How do you take best advantage of the features of the Dockerfile yet not end up with enormous images?**

Docker containers derive a part of their power because of the layered approach of a container image. You can build from existing container images and thus leverage the work done by others. Very often, such images have three large layers:

1. The base operating system image, for example a standard (vendor-built) Linux distribution image for Ubuntu, RedHat, or Fedora; 
2. The application runtime environment, for example a Java virtual machine;
3. The application itself.

The three layers inherit from each other, which makes it possible to have all "Ubuntu" applications run from a standardized image, all "Java" applications run from an image derived from that standard, and only the application binary distribution is the final layer that makes the container the application-specific container.

The benefits of standardizing these layers are many:

* Basic layers only need to be vetted once
* As a cloud server will locally cache layers (subject to disk usage policies), the basic layers for your applications are likely already on the machine when it is launched, and only the application-specific layer needs to be fetched. This speeds up upgrades and launches of new applications.

However, there are drawbacks around this as well; a lot of the drawbacks are similar to the drawbacks of deep class hierarchies in object oriented programming:

* As an application developer, you may not always know what resides exactly in the shared base layer;
* As a maintained of a base layer, you may not know all the applications that use your layer and therefore triggering upgrades after for example a security patch becomes challenging
* The deeper the hierarchy, the more complex management and correct patching policies become.

Therefore,

**Share layers between Docker images but don't go overboard with very deep hierarchies; staying with around three layers - an OS base layer, a runtime layer, and an application layer are often enough.**

Have a system in place that can find and automatically regenerate base layers. For security, keep track of what applications are using what base layers (either through tooling in your Docker registry or by scanning your version control system). Clearly and extensively tag base layers so it is clear what they contain (for example: 'ubuntu-java:14.04-1.8u123' for an image that a java application can use).
