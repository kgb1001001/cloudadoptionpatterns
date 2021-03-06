# Birthing Pool

You have a new cloud native application that is based on a container technology (such as Docker) and you want to ensure that container images with known vulnerabilities are not deployed to your environment. However, some vulnerabilities within a container image cannot be picked up by a static vulnerability scanner as they can only be found in a running container.

**How do you detect such vulnerabilities without deploying a potentially vulnerable image and into a test or production environment?**

Vulnerabilities present in a running container should be isolated to a micro-segmented network where the impact cannot be replicated to other machines. However, if we place an untested image into an environment shared with other development stages, then malware present in that image may affect those other stages.

Therefore,

**Create a new environment as part of your overall CI/CD process consisting of an isolated environment called a birthing pool.  Run dynamic vulnerability scans within this environment in order to limit the exposure of other Docker runtime environments to potential malware.**

Up to this point, we have been considering that the isolation provided by Docker itself, in that each image is functionally isolated from other images by the Docker execution environment is adequate for all types of vulnerabilities that may be found in an image.  However, that may not be true.  There is the possibility that a side-channel or Docker infrastructure attack (such as forkbomb, see [Baset](https://www.slideshare.net/SalmanBaset/unraveling-docker-security-lessons-from-a-production-cloud-70513798)) may interfere with the operation of your Docker execution environment and thus affect other Docker images. Thus the need exists to have at least two separate Docker execution environments, each segmented from the other, in order to eliminate this possibility.

An example of all of the different parts of an end-to-end Docker development process, including a separate environment for active vulnerability scanning within a birthing pool, is shown in Figure 3: Stages including Birthing Pool.
 
![Stages including Birthing Pool](https://github.com/cdegroot/cloud-patterns-book/blob/master/assets/Figure3.png) 

*Figure 3: Stages including Birthing Pool*

You should be able to create the new birthing pool environment from scratch using infrastructure as code techniques and tools, such as Terraform.  The good news about this approach is that since we are creating an uncustomized, “off-the-shelf” installation of a common runtime such as Kubernetes or Docker Enterprise, that this can be done without introducing the kind of configuration drift caused by team-level specialization we discussed earlier. The birthing pool should contain no sensitive data. This allows you to run your container within the birthing pool and allow you to run a vulnerability scan in this isolated environment and detect any vulnerabilities that can only be found through dynamic scans.
The introduction of the birthing pool means that a dynamic scan can be performed without exposing other aspects of the application estate to the vulnerability. One potential implementation of this, using separate Kubernetes clusters for each different environment in Figure 4: Isolation of the Birthing Pool.

![Isolation of the Birthing Pool](https://github.com/cdegroot/cloud-patterns-book/blob/master/assets/Figure4.png)

*Figure 4: Isolation of the Birthing Pool*

Images should pass through a Birthing Pool before they are placed by a [Docker Build Pipeline](https://github.com/cdegroot/cloud-patterns-book/blob/master/container-architecture/docker-build-pipeline.md) into an [Approved Image Repository](https://github.com/cdegroot/cloud-patterns-book/blob/master/container-architecture/approved-image-repository.md).
