**DRAFT: This isn't quite right**

Title: Single registry per deployment environment

Context:

You have developed a new solution that runs on containers that consists of multiple microservices and that lives in a larger overall eco-system of possibly hundreds of microservices.

Problem:

You are not sure whether you should be isolating your images to a single container registry or to a centralized registry.  For availability and performance reasons it is important that you have a single view of an image registry and an application only pulls images from a single registry as pulling from multiple registries decreases availability and increases fragility.

Forces:

* A single central registry that hosts all images is easy to maintain
* A single central registry means that there is no isolation from malware
* A single central registry reduces administration effort
* A single central registry means that any machine can access and spin up any image \(larger security threat\)
* Smaller decentralized registries increase size of estate and complexity
* A registry per application means the application isolated from issues in the estate.

Solution:

You should have a single image registry per deployment environment where you isolate applications through container groups.  One group should be for hosting your own applications and another for hosting cached/pulled versions of approved third party or organization base images.  Hosted container images should only be able to inherit from images in the same hosted directory or approved third parties or approved base images

Results:

A single image registry per deployment environment means:

* A
* XXX



