---
parent: Cloud Native DevOps
title: Aggregate Descriptor
---
Aggregate Descriptor
===

You are building an application that will need to run in the cloud that is composed of many parts.  You may be using a [Container Orchestrator](../Cloud-Native-Architecture/Container-Orchestrator.md) to schedule running your containers.  You want to be able to deploy your complex application into your cloud environment without having to constantly change the way in which deployment is carried out as small details (such as code versions) change.

**How do you define a reusable architecture independent of particular application artifacts?**

Useful applications are almost never composed of a single component.  At a minimum, most applications require a database, possibly require a messaging system of some sort, and may require other aspects, such as load balancers or other front-end proxy or security components.  On the cloud, it's important to describe some of the deployment metadata that allows the application to take advantage of the unique features of cloud computing, such as [Autoscaling]().  In the autoscaling case, there is a need to specify the upper and lower bounds of scaling in order to ensure appropriate resliance while not allowing the application to become too expensive to run.

The problem comes in as you start thinking about how you can bring all of these things together.  There are two possible, but inadequate solutions:

1. You could do all of the deployment and configuration manually
2. You could write deployment scripts that automate the process

Therefore,

**Define an Aggregate Descriptor of services, runtimes, and the connections between them.  This Aggregate Descriptor is executed by a Deployment Engine that reads the descriptor and creates the necessary containers and other aspects of the runtime system.**

Examples: Terraform, HELM charts, Docker Compose YML’s, Operators

