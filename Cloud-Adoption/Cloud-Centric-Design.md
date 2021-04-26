---
title: Cloud Centric Design
parent: Cloud Adoption
---
# Cloud Centric Design

Many teams are able to work within what can be termed a greenfield.  In that situation, you have a problem to solve, and also have the ability to write a brand new application (or rewrite an existing one) and the time in which to do that application development work.  When you are in that situation you still have all of the same project development issues to resolve that you have in an existing application, (e.g. you still need to balance time, cost and people) but you often have more flexibility to choose among how you will trade off each of these.

**How do you design your application to take the maximum advantage of all the features of the cloud for the best future proofing and agility?  What can a team do to make sure that they are balancing speed, cost and people utilization in the best combination?**

Therefore,

**Begin any new greenfield projects by performing a Cloud-Centric Design of your application to run natively on a cloud (PaaS) environment such as a container-based environment.**

The difference between a greenfield and a brownfield is not always clear-cut.  Especially when corporate data is part of the equation, it's often challenging to completely dissociate an application from the IT environment in which it is conceived. Nonetheless, when you have the opportunity to make a clean (or mostly clean) break from existing standards and processes, it allows you more freedom to adopt new approaches that can be more productive in the long run.

So, whenever you are developing a new application that can run in the cloud, instead of asking yourself "How do we conform to existing standards for application development" ask yourself "What can be gained by trying new approaches?"  

Some of the important considerations that you will want to consider when embracing a Cloud-Centric design include: 

* Building with Fine-grained components that give you the ability to test more easily than large monolithic components.
* Employing decoupling measures such as REST API's or Event-driven approaches to keep boundaries between components clean.
* Minimizing the use of state (it is impossible to entirely eliminate state, but you should only keep the state that is absolutely required).
* Following a zero-trust model to minimize privileges for security.
* Practicing Immutable deployment models to remove runtime changes and eliminate runtime administration. 

As a result of addressing these considerations, a Cloud-Centric Design would embrace the following approaches:

* It would be based on the [Microservices Architecture](../Microservices/Microservices-Architecture.md) in order to minimize the Blast Radius of any code changes.
* It might take advantage of [Polyglot Programming](../Microservices/Polyglot-Development.md) in order to make sure that the right languages and development tools are chosen for each part of the job. 
* It would take advantage of [Scaleable Stores](../Scalable-Store/Scalable-Store.md) that allow development teams to match the data storage technology to the type of data that being stored and to the data storage and retrieval patterns that are most prevalent for that application
* It can take advantage of [Cloud DevOps](../Cloud-Native-DevOps/README.md).

