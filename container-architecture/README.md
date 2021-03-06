# Introduction

This part of our pattern language is concerned with the problems inherent in building and delivering software using Containers,
particularly those issues that arise during the process of mapping docker images and containers into the stages of a software development
lifecycle. The language assumes that the reader will be building applications following an agile approach that is characterized by 
Continuous Integration/Continuous Delivery

Containers are one of the most rapidly adopted software technologies of the last several years, with extraordinary growth in adoption (see [PortworxSurvey](https://portworx.com/2017-container-adoption-survey/)). This rapid adoption is the result of an impressive increase in developer productivity and ability to delivery cost reduction resulting from container adoption (see [Synopsis](https://www.synopsys.com/blogs/software-security/container-adoption-numbers/)).

Containers are a way of packaging software that provides a lightweight mechanism for bringing application code and configuration together with all of the software prerequisites (such as a language runtime, an application server, or libraries) that the application depends on.  Containers differ from traditional virtualization platforms in that the container does not include the entire guest OS, but instead relies on the services of the container platform to provide isolation from other processes running within the container platform.  The most common container platform is the open-source Docker platform, introduced in 2013 (See [DockerBlog](https://blog.docker.com/2014/06/its-here-docker-1-0/)). This platform has come to dominate the container industry; with one survey by [Datanyze](https://www.datanyze.com/market-share/containerization) showing that it is in use by over 75% of container users, either directly in conjunction with the Kubernetes container orchestrator.   The patterns in this pattern language have thus been written with the Docker platform in mind, although it is conceivable that they would also apply to other container platforms.

In Docker, a container (which can be thought of as a running instance of a software package and code) is implemented as an isolated user space running within a running Linux OS (a Docker host), while the platform provides a shared kernel across containers running within that OS.  All software packages and data in a container are isolated at run time.  Resource management is implemented with Unix cgroups while resource isolation is provided through namespaces.  Filesystem isolation is managed through the Docker file system, which is an additive, or union, filesystem using copy-on-write semantics. 
 

# Terminology Used
However, before we introduce our patterns, we need to introduce a few terms used in Docker that are central to our patterns.  First, as we have already discussed, a container is a running instance of software executing within the Docker environment.  The combination of 
software packages, code and associated prerequisites is packaged within docker as an image.  

The image is an individual instance of a layered file system where each layer builds on top of the layers below it. An example (showing specific application server software, applications and a particular operating system release) is shown below. (See Figure 1: Layers in Docker).  

![Layers in Docker](https://github.com/cdegroot/cloud-patterns-book/blob/master/assets/Figure1.png)

*Figure 1: Layers in Docker*

Images are defined by build files called dockerfiles. A dockerfile begins with an existing image as the starting point and provides a set of instructions to augment that image (each of which results in a new layer in the file system).  It also includes meta-data such as the ports exposed and the command to execute when the image is started. Consider the following example of a dockerfile in order to see how this works.

`# Pull base image.`

`FROM ibmnode:v6`

`MAINTAINER Chris Hay <chris.hay@uk.ibm.com>` 

`# Install Java.`

`RUN apt-get update && \ `

`apt-get upgrade -y && \ `

`apt-get install -y software-properties-common && \ `

`add-apt-repository ppa:webupd8team/java -y && \ `

`apt-get update && \` 

`echo oracle-java8-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \ apt-get install -y oracle-java8-installer && \` 

`apt-get clean` 

`# Define working directory.` 

`WORKDIR /data` 

`# Define commonly used JAVA_HOME variable` 

`ENV JAVA_HOME /usr/lib/jvm/java-8-oracle`

*Listing 1: Example dockerfile for Java*

The dockerfile above takes an existing Node.JS base image and creates a new image that includes the Java 8 runtime.  The dockerfile will use the ibmnode (version 6) base image as a starting point and will then download and install the Java 8 runtime from Oracle.

A Docker registry is a service for storing and retrieving Docker images.  You can think of it as being like a source-code control system (e.g. Git) for docker images.  There are two general types of registries; a public registry is one that provides this service to many customers where the images are publicly available and searchable.  Examples of this include Docker Hub, the Amazon Elastic Container Registry, and the IBM Container Registry service.  A private registry is one that serves a single customer. Both types of registry may be cloud hosted, although private registries are sometimes also deployed on premises.  For instance, in Docker you can deploy your own registry services and store your images locally or in any other location running docker (such as a hosted private cloud).

A Docker repository is a collection of related docker images that have unique tags.  A tag is an alphanumeric identifier for an image within a repository.  For instance, Docker Hub allows you to create new repositories via the “Create Repository” function.  This named repository then becomes a common name that is used as part of the identifier of images within a docker push or docker pull, e.g. *docker push user/repository-name:tag*.  Other registries also support similar approaches to creating repositories.


# Patterns in this section

+ [Docker Build Pipeline](https://github.com/cdegroot/cloud-patterns-book/blob/master/container-architecture/docker-build-pipeline.md) is the root pattern of this pattern language.  A DevOps pipeline is a core concept for Continuous Integration/Continuous Delivery.  An issue many teams face is where to introduce docker into their delivery processes.  Starting with an automated delivery pipeline for building and deploying your docker images leads to the other patterns in this section.
+ [Pipeline Vulnerability Scanner](https://github.com/cdegroot/cloud-patterns-book/blob/master/container-architecture/cicd-pipeline-vulnerability-scan.md) enables you to perform static vulnerability scans as a stage within your [Docker Build Pipeline](https://github.com/cdegroot/cloud-patterns-book/blob/master/container-architecture/docker-build-pipeline.md) in order to scan your container image(s) for any known vulnerabilities and stop the deployment and report the issue if any issues are found.
+ [Registry Vulnerability Scanner](https://github.com/cdegroot/cloud-patterns-book/blob/master/container-architecture/registry-vulnerability-scanner.md) gives you the ability to scan images *after* they are built, so that new vulnerabilities that are detected after a build can be detected and addressed.
+ [Multiple Vulnerability Scanners](https://github.com/cdegroot/cloud-patterns-book/blob/master/container-architecture/multiple-vulnerability-scanners.md) addresses the issue that different vulnerability scanners use different approaches and pull threats and malware definitions from different repositories.  Teams should hedge their bets by scanning images in multiple ways.
+ [Birthing Pool](https://github.com/cdegroot/cloud-patterns-book/blob/master/container-architecture/birthing-pool.md) is a way to avoid placing an untested image into an environment shared with other development stages, allowing malware present in that image to affect those other stages.
+	[Public Image Registry](https://github.com/cdegroot/cloud-patterns-book/blob/master/container-architecture/public-image-registry.md) is a solution for making images available to others who may be outside of your development organization.
+ [Private Image Registry](https://github.com/cdegroot/cloud-patterns-book/blob/master/container-architecture/private-image-registry.md) is a solution for making images available to those within your organization, particularly useful in cases of intellectual property restriction or security restriction.
+ [Approved Image Repository](https://github.com/cdegroot/cloud-patterns-book/blob/master/container-architecture/approved-image-repository.md) is the location for approved images once they have been through the scanning and vetting process.
+ [HA Container Registry](https://github.com/cdegroot/cloud-patterns-book/blob/master/container-architecture/highly-available-container-registry.md) is important because a registry is only useful when it can be accessed.  Encountering a single point of failure on docker host startup will result in your entire Docker architecture being unavailable. 
+ [Public Registry Proxy](https://github.com/cdegroot/cloud-patterns-book/blob/master/container-architecture/public-registry-proxy.md) is a way of improving performance of image pulls in some use cases by locally caching images nearer to the Docker hosts.
