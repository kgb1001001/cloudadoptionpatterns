# HA Container Registry

You have an Service Level Agreement (SLA) for your cloud application (such as 99.99 availability) and you need to ensure that you meet your SLA's and that you have a fast time to recovery.

The issue is that in the cold start of a container host, the local cache of the host's image registry will be empty and will require the host to refetch any images from the container registry.  This situation is even more likely in a disaster recovery scenario (as it's likely that hosts will have been restarted).

**How do you ensure that your container startup will not fail at the worst possible time by having them rely on an unreliable image registry?**

The SLA on the overall solution will dictate how much effort you need to put into the availability of your registry solution.  A key factor in that is the pull time of an image from a container registry; for instance if the average pull time of an image is significantly greater than the Return To Operations (RTO) objective of your registry, then you will not notice disruptions lasting less than the RTO.  A potential complication to determining how well you can meet your overall solution SLA is that a Container Registry as a Service provider may or may not have it's own SLA

Therefore:

**Ensure that the container registry has high availability (e.g. has been redundantly deployed in a multi-region, multi-availability zone way) with a matching SLA.**  

This is a best practice that has been documented for Docker in several places such as [Labourdy](http://www.blog.labouardy.com/highly-available-docker-registry-on-aws-with-nexus/). Many companies advertise commercial container registries (such as [Portworx](https://docs.portworx.com/applications/docker-registry.html)) that are highly available, but it is rarely stated why you should care that this is so.  You should also ensure that you are using a [Public Registry Proxy](public-registry-proxy.md) in your container registry to ensure fast fetches of 3rd Party Images.  You should also ensure that your cloud provider (or if managed by your client organisation) is able to meet the SLA's that you are committing to.  If the container registry is dead and your cache is cleared then you've just lost that data center.

Ideally you should follow practices of bulk-head isolation and ensure that you have isolated and affinitized registries to your regions.  In that way, if you lose your registry then it's only lost for a single region, not for every region.  Of course, the affinity should only extend to those cases where it is required for performance reasons; if you can fetch an image from a distant registry when your local registry is down and that can still be done within your overall solution SLA, that is a valid option.

Using a High Availability Registry (with matching SLA) for a container registry (including a [Public Registry Proxy](public-registry-proxy.md)) will ensure that the Image registry remains available even in a disaster scenario. Likewise you will experience increased availability of the image registry, as there will only be a single dependency instead of depending upon multiple providers, each with different SLA’s.
