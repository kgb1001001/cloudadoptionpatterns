# Private Image Registry

You have developed a new internal application that will run on containers and you need to host the image in a container image registry so that the container technology (such as Docker) can pull and run the image on your container environment.

**How do you gain the benefits of a Public Image Registry (such as Docker Hub) without making all of your images available to the general public?**

There are several reasons why you may not be able to use a Public Image Registry.  As noted in that pattern, your image may have to contain private information such as license keys or internal network structures.  In this case, making your image available in the public would expose your architecture and make it more likely that your system will be hacked.  Likewise, you may not want to reveal IP or secrets; if it is made available to the public, there is always a risk your image could be reverse engineered.

Therefore:

**Host your container images in a Private Image Registry such as Nexus, or a private registry of your cloud platform.  The Private Image Registry supports all the same protocols and behaves exactly like a Public Image Registry.  This means that you have to configure your container servers to pull from the URI of the Private Image Registry instead of the default Public Image Registry (e.g. Docker Hub).**

Using a Private Image Registry gives you all the benefits of a public registry but keeps your container images private and secured from users or applications that you should not have access to it.  

This pattern has been described as a best practice by many different organizations, such as [BobCares](https://bobcares.com/blog/docker-private-repository/) [CenterDevice](https://blog.codecentric.de/en/2014/02/docker-registry-run-private-docker-image-repository/.) and  [Macadamian](http://www.macadamian.com/2017/02/07/creating-a-private-docker-registry/).
