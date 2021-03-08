# Approved Image Repository

You have developed a new internal application that will run on containers.  The solution has dependencies on third party images hosted in a [Public Image Registry](public-image-registry.md).  In general, developers should not have to worry about the use of third party images.  However, there is a balance that needs to be struck between ease of use and security.

**How do you prevent random images, or multiple versions of existing images, from being pulled from a [Public Image Registry](public-image-registry.md) making your overall Docker installation estate more vulnerable and harder to maintain and operate?**

In general, you want to give developers the freedom to use open-source images from the Internet.  However, this freedom comes at a cost.  For instance, a complete lack of governance could mean that you have multiple versions of an operating system across many applications - all of which would need to be tracked, maintained and patched.

Licensing is also a potential issue.  An unapproved image could be used which could create an open-source licensing issue for your application.  Likewise, an unapproved image could be used which could create a commercial licensing issue for your organization.

Maintenance of unapproved images can also cause a potential problem. A team may inadvertently create a dependency on an ungoverned image from an amateur programmer that may not maintain it, or an ungoverned image could disappear and then cause your application to fail.

Finally, security is an issue; an ungoverned image dependency could be modified and have malware installed on it.

Therefore:

**Create an Approved Public Image Repository within your [Private Image Registry](private-image-registry.md) where you have pre-downloaded all images and versions that are approved to be used in your estate.  You should lock down your container hosts so that they cannot pull images directly from Public Image Registries and must come through your Private Image Registry.  Only approved image registry administrators should be able to add images to the repository.**

It is critically important that images should be run through a [Pipeline Vulnerability Scanner](cicd-pipeline-vulnerability-scan.md) (in fact, they should be run through [Multiple Vulnerability Scanners](multiple-vulnerability-scanners.md)) before they would be added to the Approved Public Image Repository.  That ensures that developers can begin from a starting point that is known to be secure.  

The governance of the Approved Public Image Repository can be configured at multiple levels including:

* Organization
* Program
* Project
* Application

Many [Private Image Registry](private-image-registry.md) solutions possess the ability to configure such patterns and rules as part of the product.

Using an Approved Public Image Repository increases the security and governance of your solution while giving developers the freedom to use the best of breed tools and open-source images.  
