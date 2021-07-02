---
parent: Container Building
title: Least Privilege
---
# Least Privilege

You are building a container image that includes third party code (perhaps open source libraries, or a third party application).  You want to ensure that this code running in your container cannot access resources that it is not supposed to be able to access (such as the file system of the host).

**How do you ensure that your containers are not open to container privilege escalations?**

Privilege escalation is the process of obtaining more permissions for a resource (such as a process).  Malicious code does this through exploiting weaknesses in different entry points into the Linux kernel.  While code scanners can usually detect known vulnerabilities and malicious code in third party libraries, it only takes one undetected zero-day exploit to render your system insecure.

Therefore,

**Follow the principle of least privilege.  A process should have only those access rights that are needed to accomplish each task and no more.**

1. Build an image that combines everything by privilege level to minimize the possibility of escalations.  
2. Create a dedicated user and group in the Docker image for the application using the USER directive.  
3. Never execute a process from the image as root.

The last two are especially important in limiting the possibility of privilege escalation.  First of all, begin by creating the user and group in the Dockerfile.  An example of this is would be to use:

    RUN groupadd -r postgres && useradd --no-log-init -r -g postgres postgres
    
 Next, you want to use the USER command to change to the non-root user you just created.
 
    USER postgres
     
The downside (if it can be considered a downside) of this approach is that this will only work if the process can run without root privileges.  However, requiring root privileges in Unix or Linux can be considered a bug for most software.  However, if a preparation or build step requires escalated privileges, then you can perhaps consider combining this pattern with [Multistage Build](multistage-image-build.md) to escalate privileges in the temporary build image that is created, and then only using the newly created user (with fewer privileges) in the final production image that the build creates.  In any case, you want to avoid constantly switching users within your Dockerfile - you want to avoid switching users at all if you can, and if you cannot, at least group all of the commands that have to execute under a particular user together.

Building images up from standardized [minimal base images](minimal-base-image.md) is a way of minimizing the amount of privileges you need to grant in that there is less of a need for additional process execution during the build phase.
