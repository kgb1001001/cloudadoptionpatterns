# Least Privilege

**How do you ensure that you are not open to container privilege escalations?**

**Build an image that combines everything by privilege level to minimize escalations.  Create a dedicated user and group in the Docker image for the application using the USER directive.  Never execute a process from the image as root.**
