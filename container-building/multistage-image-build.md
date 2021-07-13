---
parent: Container Building
title: Multistage Build
---
# Multistage Build

You are building an application with containers.  You have a complex build process that requires several tools to complete the build.  However, these tools are no longer needed once the container has been built, as they are not required at runtime.

**How do you keep the size of your docker files down to a manageable level, and at the same time reduce the potential attack surface of your docker containers by making sure that they only contain what is absolutely necessary?**

Let’s consider the following problem.  You are building a Minecraft server that has a special plugin that allows for an online agent to participate in chats.  Now, creating a Minecraft server may seem like a frivolous example, but in fact, Minecraft is one of the most commonly used Java applications in existence, with an extensive development community, and has a build and extension process that is quite similar to many Enterprise applications written in Java.  As a result, it makes a nice stand-in for a complex Enterprise application.  In order to extend Minecraft, you run the base Minecraft server along with a predefined “plugins” directory - very similar to the extension process for Eclipse or many other applications written in Java.

The process to building a server in Linux is:

1. Install the JDK
2. Install a tool (such as wget) that can fetch the latest JAR file used for building the Server
3. Install Git (used by the Build JAR to fetch the latest code)
4. Run the Build Jar at the Java command line

After the Build Jar has run, a new server Jar file (named spigot-<version>.jar) is created.  That Jar file looks in the "plugins" directory for other Plugin Jar files when it executes.  

This process has been encoded in the Dockerfile below:

    FROM ubuntu:20.04
    MAINTAINER Kyle Brown “brownkyl@us.ibm.com”
    RUN apt-get update
    RUN apt-get install -y git
    RUN DEBIAN_FRONTEND=noninteractive apt-get install -y default-jdk
    RUN apt-get install -y wget
    RUN mkdir minecraft
    RUN wget "https://hub.spigotmc.org//jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar" -O minecraft/BuildTools.jar
    RUN git config --global core.autocrlf input
    RUN java -jar minecraft/BuildTools.jar --rev 1.16.1
    RUN echo "eula=true" > eula.txt
    RUN mkdir plugins
    ADD HelloWorld.jar /plugins/HelloWorld.jar
    CMD java -XX:MaxPermSize=128M -Xms512m -Xmx1024m -jar spigot-1.16.1.jar nogui
    EXPOSE 25565

Now here’s the issue we have to consider - we’ve just added multiple tools to the image that are not needed at runtime!  A version of Java will still be needed in the final image - not only is is needed for the build stage, but also to invoke the Java command to start the Minecraft server at the end.  However, the JDK is not really needed - instead, a JRE (which adds 239MB less to an image size) would suffice.  Git is not needed in the end, nor is wget, both of which could potentially contain vulnerabilities that could be exploited.

Now, one way you could do this (which was actually common early in the development of docker images) is to combine all of the commands to obtain a tool, use a tool and then delete the tool (and its associated artifacts) in one long Unix command line.  An example of this is shown below

    FROM ubuntu:20.04
    MAINTAINER Kyle Brown “brownkyl@us.ibm.com”
    RUN apt-get update &&\
	    apt-get install -y git &&\
	    DEBIAN_FRONTEND=noninteractive apt-get install -y default-jdk &&\
	    apt-get install -y wget &&\
	    mkdir minecraft &&\
	    wget "https://hub.spigotmc.org//jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar" -O minecraft/BuildTools.jar &&\
	    git config --global core.autocrlf input &&\
	    java -jar minecraft/BuildTools.jar --rev 1.16.1 &&\
	    rm -r Bukkit &&\
	    rm -r CraftBukkit &&\
	    rm -r Spigot &&\
	    rm -r BuildData &&\
	    rm -r work &&\
	    rm -r minecraft &&\
	    apt-get purge -y --autoremove git wget
    RUN echo "eula=true" > eula.txt &&\
    mkdir plugins
    ADD Tutorial.jar /plugins/Tutorial.jar
    CMD java -Xms512m -Xmx1024m -jar spigot-1.16.1.jar nogui
    EXPOSE 25565

However, this is an unsatisfactory solution in a number of ways.  Not only is it possible to leave tools behind (for instance in this instance, note that the script cleans up wget, but leaves Git behind installed in the image) but it is difficult to debug problems when they occur.  

Therefore,

**Use a multistage build that only retains the final outputs of the build process in the resulting container.  Likewise, fetch and manage both build tools and secrets in an intermediate image layer that is discarded along the way.**

Docker engine 17.05 introduced the idea of a “multistage build” that effectively creates a throwaway image that can be used for the build step, is accessible long enough to copy out the relevant built artifacts, and then is destroyed.  This required a little additional syntax to the FROM command, allow you to first of all declare a second image (with an additional FROM command in the Dockerfile) and then also to allow you to reference that intermediate image from the final image with the COPY command. 

    FROM ubuntu:20.04 AS builder
    MAINTAINER Kyle Brown “brownkyl@us.ibm.com"
    RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
        default-jdk \
        git \
        wget
    WORKDIR minecraft
    RUN wget "https://hub.spigotmc.org//jenkins/job/BuildTools/lastSuccessfulBuild/artifact/target/BuildTools.jar" -O BuildTools.jar
    RUN java -jar BuildTools.jar --rev 1.16.1

    FROM ubuntu:20.04
    RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y default-jre
    WORKDIR minecraft
    COPY --from=builder /minecraft/spigot-1.16.1.jar .
    RUN echo "eula=true" > eula.txt
    RUN mkdir plugins
    ADD Tutorial.jar /plugins/Tutorial.jar
    CMD java -Xms512m -Xmx1024m -jar spigot-1.16.1.jar nogui
    EXPOSE 25565

Note that what happens is that this Dockerfile separates the process of creating an image for building the Jar file (the top half of the file, which is defining the “builder” image) from the process of creating an image to run the resulting file (the bottom half, which is what is returned from docker build as the final image).  The difference in size is stark.  The previous Dockerfile, when built, results in an image which is 907MB in size.  The second Dockerfile results in an image which is only 556MB in size.   Given that one of the main reasons why you choose to use Docker images is the ability to pack in more instances in the same amount of memory, in this example you’ve just roughly doubled the number of containers built from this image that can be run on the same Kubernetes node. 
	
In order to control the overall size of the image, you want to begin from a [Minimal Base Image](minimal-base-image.md).  You always need to follow the principle of [Least Privilege](least-privilege.md) when starting processes and requesting access to resources.
