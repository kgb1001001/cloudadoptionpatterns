---
parent: Container DevOps
title: Single Image Registry
---
Title: Single Image Registry

Context:

You have developed a new internal application that will run on containers.  The solution has dependencies on third party images hosted in a _Cloud Hosted Registry_.

Problem:

Although you have no issue with the usage of the third party images \(they are approved images for usage\), you are concerned about the overall performance, availability and the increased attack surface of your estate by creating a depenency on several _Public Image Registries_ where there are no SLA's.  How should you handle access to these images?

Forces:

* The container images are quite large and take significant time to pull
* There are SLA's on the overall solution including the CI/CD pipeline
* There are SLA's on the time to recover in a disaster recover scenario
* Security is paramount and locking down external access for container hosts is important
* Auditing and governance of which container images \(and versions\) are used across the estate

Solution:

You should ensure that the applications within your estate only pull from a single registry rather than multiple registries.

This can be achieved through the following methods:

* Using a _Public Registry Proxy_ as part of your Image Registry
* Using an Approved Public Image Repository as part of your Image Registry

Results:

Using a single image registry will increase the overall availability of your solution as all container images are stored locally on your container registry meaning that if you need to pull your container \(such as a restart of the container host\) then the local server cache does not need to pull the image from other registries.  In addition this increases the security of your environment as access to the outside world can be locked down \(i.e. each server will not require a connection to the public hub\).  Finally this will increase the overall availability of the solution as there are less dependencies on external clouds.

