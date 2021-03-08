# Public Image Registry

You have developed a new container image that you wish to make available to the wider development community.  This may be a new container image you wish to make available to your customers, a new open-source application that you wish to make available, or an improved installation of an existing open-source product that you wish to contribute back to the community.

In each of these cases, you should assume that there is no IP restriction and that you wish to make the image available publicly.  Likewise, there should be no commercial or licensing implications to distributing the image.

**How do you make all supported versions of your image available to the general public in a manner that allows you to easily fix bugs or vulnerabilities, distribute new versions and simplify installation?**

There are several reasons that lead developers to want to use Docker images in the first place.  For instance, many commercial development teams have high support costs because customers incorrectly install software installations due to complex instructions.  

Likewise, development teams wish to be able to quickly and reactively provide frequent patches to existing versions with minimal impact.  Critical to this is the ability to distribute new versions of your application and make them available quickly and securely.

Therefore:

**Publish all supported versions of your image, correctly tagged with the right version, to a Public Image Registry such as Docker Hub.   By centralizing the image distribution you are able to harden the image, fix images, fix bugs and then provide an updated version of the image for your application as you fix issues.** 

If you need to release a new version of your application then you are able to tag the new version of your image and make it available immediately allowing consumers to choose when they should use the new version of your application.

Consumers of your image will be able to just pull the version of the image that they need instantly without having to perform any complex installations.

Publishing images to a Public Image Registry allows you to centralize the distribution of your application in a secure manner and allows you to provide frequent releases of your application or image in a secure fashion for those images that can publicly distributed.  However, the benefits of a Public Image Registry can only be realized if it is available, thus the need for an [HA Container Registry](highly-available-container-registry.md).

When publishing images to a public registry you should ensure that in your published image that you don't break any licensing concerns by using unlicensed software or IP, and that you do not include any sensitive data such as Keys, Passwords, Infrastructure information such as internal IP's in your images.  Any requirement to include these types of information in your images will instead require you to use a [Private Image Registry](private-image-registry.md) instead.

Likewise, you will want to use a [Pipeline Vulnerability Scanner](pipeline-vulnerability-scanner.md) to ensure you don't pass vulnerabilities to consumers of your images. 
