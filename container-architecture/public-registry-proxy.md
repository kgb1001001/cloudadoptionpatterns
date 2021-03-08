# Public Registry Proxy

You have developed a new internal application that will run on containers.  The solution has dependencies on third party images hosted in a Public Image Registry.

**How should you handle access to images in Public Image Registries when you are concerned about the overall performance, availability and the overall attack surface of your estate?**

Although you have no issue with the usage of the third party images so long as they are approved for usage, pulling these images from a Public Image Registry can have several issues.  First, many images are quite large and take significant time to pull.  Second, there are SLA's on the overall solution including the CI/CD pipeline.  Finally, there are SLA's on the time to recover in a disaster recover scenario that must also be met.

In addition, in many situations, Security is paramount and locking down external access for container hosts is important.  In these situations, Auditing and governance of which container images (and versions) are commonly used across the estate

Therefore:

**Configure your Private Image Registry to proxy all images from the public repositories rather than allowing the container hosts to pull the images directly from the Public Image Registry.**

Using a Public Registry Proxy will increase the overall availability of your solution as all container images are cached locally on your container registry meaning that if you need to pull your container (such as a restart of the container host) then the local server cache does not need to pull the image from the [Public Image Registry](public-image-registry.md).  In addition this increases the security of your environment as access to the outside world can be locked down (i.e. each server will not require a connection to the public hub).  Finally this will increase the overall availability of the solution, as there are fewer dependencies on external clouds.

