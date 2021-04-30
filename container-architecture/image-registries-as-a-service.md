---
parent: Container DevOps
title: Cloud Hosted Image Registry
---
Title: Cloud Hosted Image Registry

Context:

You have developed a new internal application that will run on containers and you need to host the image in a container repository so that the container technology \(such as docker\) can pull and run the image on your container environment.

Problem:

You are unsure if you should use a _Cloud Hosted Image Registry_ or whether you should create your own _Private Image Registry_ within your PAAS or IAAS environment.

Forces:

* You don't have any contractual SLA's where you must guarantee the availability of your overall solution
* There are no restrictions for legal reasons on the location for hosting of the container images
* There are no security or sensitivities on hosting the container images outside of your environment
* Hosting your own registry increases operational maintenance \(Backup, Restore, Patching\)
* Hosting your own registry increases infrastructure estate \(volumes, firewalls, load balancers\)
* Hosting your own registry increases testing \(availability, DR, performance\)
* Creating additional infrastructure increases time to market, cost and project timelines
* Additional Infrastructure and application estate opens up a wider threat surface area,

Solution:

You should host your container images in a _Cloud Hosted Image Registry_ \(such as IBM Cloud, docker cloud, google, quay\) rather than attempting to roll your own solution.  You should only roll your own image if there is somer sort of NFR that prevents you from using a cloud service.

Results:

Using a _Cloud Hosted Image Registry_ speeds up your time to market and reduces your operational spend by focusing on your application rather than focusing on scaffolding.

