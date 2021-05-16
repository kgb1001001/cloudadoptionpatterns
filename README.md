---
title: Patterns for Developers and Architects building for the cloud
nav_order: 1
permalink: /
---
# Patterns for Developers and Architects building for the cloud

This is a work in progress.  We hope you will find it useful even in its infancy as we continue to build out this site.

This project began as a series of (loosely) related papers submitted to the PLoP conference in 2016 - one by [Kyle Brown](Kyle-Brown-bio.md) and [Bobby Woolf](Bobby-Woolf-bio.md) and another by [Cees De Groot](Cees-De-Groot-bio.md) - at the conference we decided to explore the idea of joining the two papers into a common pattern language.  Container DevOps Patterns from a PLoP 2018 paper by Kyle Brown and [Chris Hay](Chris-Hay-bio.md) were added to the growing language, and likewise Kyle also added a set of Event-based systems patterns from a 2006 paper Kyle co-wrote for an internal IBM conference. [Joseph Yoder](Joseph-Yoder-bio.md) also joined the collaboration, adding Quality Delivery Pipeline patterns from SugarLoafPLoP 2018, Deployment Patterns for Confidence from AsianPLoP 2019, and a set of Strangler Patterns extracted from a PLoP 2020 paper.

This set of patterns is intended for use by Architects, Lead Developers or Senior Developers who are thinking about adopting the cloud, especially as they evolve toward a cloud-native architecture in their projects.  It is intended to provide guidance on how cloud-native applications should be designed, how they fit into a larger architectural picture, and how they can be built to operate efficiently.  This version specifically addresses issues of systems design, microservices design and microservices efficiency, security and  development process.  They are currently being evolved, but we have developed at least a basic point of view on each section.

+ [Cloud Adoption](Cloud-Adoption/README.md) is the place to start the journey.  It contains a set of patterns about the different architectural approaches needed to build new cloud-native applications or to evolve existing applications toward a cloud-native approach.
+ [Cloud Client Architecture](Cloud-Client-Architecture/README.md) is a good place to go next.  It starts at the top of the application tree - with a discussion of current client-side application patterns that facilitate cloud-native development.
+ [Cloud Native Architecture](Cloud-Native-Architecture/README.md) is the logical continuation of the story. It begins to explore the process patterns for identifying microservices and events.
+ [Microservices](Microservices/README.md) then brings in the set of patterns for implementing the microservices found by following the process patterns in the previous section
+ [Strangler Patterns](Strangler-Patterns/README.md) are important in making the transition from a traditional monolithic architecture to Microservices.
+ [Event Based Architecture](Event-Based-Architecture/README.md) is the core set of patterns for building microservices that are oriented around event processing.
+ [Coexistence patterns](Coexistence-Patterns/README.md) provide guidance for teams implementing Microservices and Event Based Architectures when there is the need to coexist with an existing system for an extended period of time.
+ [Scalable Store](Scalable-Store/README.md) contains the patterns for identifying the right persistence architecture and persistence mechanism for a particular microservice implementation.
+ [Cloud Native DevOps](Cloud-Native-DevOps/README.md) introduces the DevOps conversation by discussing many of the fundamental patterns around developing, testing and managing a cloud-native architecture.
+ [Container DevOps](container-architecture/README.md) continues the discussion of DevOps by introducing patterns around building a DevOps pipeline for and managing the containers that your microservices will be deployed into.
+ [Organization and Process Patterns](Organization-Process/README.md) are required to provide the constraints that team size and composition put on the types of practices that teams can implement.

The relationship between the different sets of patterns in this language are shown below:


![Overview](/assets/LanguageOverview.png)
