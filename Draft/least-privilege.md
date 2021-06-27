# Least Privilege

You are building a container image that includes third party code (perhaps open source libraries, or a third party application).  You want to ensure that this code running in your container cannot access resources that it is not supposed to be able to access (such as the file system of the host).

**How do you ensure that your containers are not open to container privilege escalations?**

Privilege escalation is the process of obtaining more permissions for a resource (such as a process).  Malicious code does this through exploiting weaknesses in different entry points into the Linux kernel.  While code scanners can usually detect known vulnerabilities and malicious code in third party libraries, it only takes one undetected zero-day exploit to render your system insecure.

Therefore,

**Follow the principle of least privilege.  A process should have only those access rights that are needed to accomplish each task and no more.**

1. Build an image that combines everything by privilege level to minimize the possibility of escalations.  
2. Create a dedicated user and group in the Docker image for the application using the USER directive.  
3. Never execute a process from the image as root.
