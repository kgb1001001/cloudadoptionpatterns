---
title: Containerize The Monolith
parent: Cloud Adoption
---
# Containerize The Monolith

You are migrating an existing system into the Cloud.  Your application is relatively up-to-date, in that it is based on versions of standards and frameworks (such as JEE or Spring) that are supported by recent versions of middleware.  What's more, your middleware vendors support a containerization strategy.

**What is the best approach for moving to the cloud quickly, but still giving you the flexibilility to do development or deployment on-premises?**

Most traditional application development has been done on bare-metal hardware or in VM's.  However, in the last few years, a new option has emerged; container platforms like Docker.

Containers have several advantages over VM's. Notably, a Docker container will run identically on any host, anywhere, that supports Docker.  that means that when you containerize an application that you have maximal flexibility in where to deploy your application.  By contrast, VM's are not nearly as portable - a KVM VM image will not run natively on AWS or in a VMWare-based private cloud.

However, not all middleware is supported in containers.  Even when a vendor (such as Red Hat or IBM) supports middleware on containers, they generally only support relatively recent versions of that middleware.  If your application is running on an older version, either you are on your own in trying to containerize the middleware (often running into support issues) or it simply will not run on containers at all.

But when you find yourself in that sweet spot where your application is compatible with a vendor-supported middleware stack, you have more options than you otherwise would.  

Therefore,

**Containerize your monolithic application as a first step onto the cloud.  You can continue to run your application on-prem in Docker if needed, but this allows you to move to multiple public and private cloud options over time.**

*Containerizing the Monolith* is better option for those cases where a [Lift-And-Shift](Lift-And-Shift.md) will result in more work over time, e.g. when the application is being actively maintained and will eventually need to be moved to the cloud or refactored.  However, containerization is only an option when the application itself is maintained by an application team; COTS applications are not good candidats for containerization in most cases because the vendors will not support them in that form.

*Containerizing the Monolith* is often only a half-step, however.  In some cases, particularly small monoliths, if the team is able to deliver features at the rate and pace you need, then containerization may be the final step in your journey to the cloud.  However, for larger monoliths where the complexity of the monolith and/or testing time makes it impossible to deliver features at the rate needed, you will still want to look at [Cloud Refactoring](Cloud-Refactoring.md) over time as that will result in the best overall value if the application is sufficiently complex to warrant division into microservices.  In any case, once you decide to adopt containers, you will need to deal with the changes to your DevOps  processes tha containerization will warrant by moving to a [Container Build Pipeline](../container-architecture/docker-build-pipeline.md).
