Title: Container Registry Operational Testing

Context:

You have developed your new cloud native application and you want to ensure that your solution is operationally ready. 

Problem:

What sort of testing should i perform to ensure that performance, availability and security needs are met for the container registry?

Forces:

* Is there any monitoring on the Container Registry itself, are you alerted if it's unavailable
* Is there a single point of failure between the container registry and the container
  * What happens if you lose internet access
* What happens if I kill the cache on all my container hosts
  * How long will it take to pull all the container images from fresh
* Are the image registries affinitized to the data center? 
  * * if you lose one container registry then you lose them all?
* Have you had a security review on the images?  
  * Are you exposing some secrets in the image \(password and keys\)?
  * Are you leaking internal information?
* Is the registry backed up?
* Is the registry locked down?  
  * Can i pull an application from the registry onto another part of the estate?
  * Are we sure only appropriate users / pipelines can push into the registry 

Solution:

You should ensure that your container registry is treated as a first class citizen of your infrastructure

This means it should be:

* Performance Tested
* High Availability \(multi-region and affinitized to regions\)
* Chaos Monkey Style Tested
* Tested for Disaster Recovery Scenarios
* Monitored
* Secured

Results:

By treating the Container Registry as a first class citizen of your solution then when the scenario occurs that you lose access to your container registry \(or in a disaster scenario where you lose an entire region\) then you know that your container registry has been tested and won't be lost in the same scenario.  In addition you can be sure that you don't end-up creating an additional threat vector by allowing hackers to penetrate your system by injecting malicious images through your registry.

