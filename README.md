# Introduction

This is a work in progress.

This set of patterns is intended for use by Architects, Lead Developers or Senior Developers who are thinking about adopting the cloud, especially as they evolve toward a cloud-native architecture in their projects.  It is intended to provide guidance on how cloud-native applications should be designed, how they fit into a larger architectural picture, and how they can be built to operate efficiently.  Tihs version specifically addresses issues of systems design, microservices design and microservices efficiency, security and  development process.  They are currently being evolved, but we have developed at least a basic point of view on each section.

+ [Cloud Adoption](https://github.com/cdegroot/cloud-patterns-book/tree/master/Cloud-Adoption/README.md) is the place to start the journey.  It contains a set of patterns about the different architectural approaches needed to build new cloud-native applications or to evolve existing applciations toward a cloud-native approach.
+ [Cloud Client Architecture](https://github.com/cdegroot/cloud-patterns-book/tree/master/Cloud-Client-Architecture/README.md) is a good place to go next.  It starts at the top of the application tree - with a discussion of current client-side application patterns that faciliatate cloud-native development.
+ [Cloud Native Architecture](https://github.com/cdegroot/cloud-patterns-book/tree/master/Cloud-Native-Architecture/README.md) is the logical continuation of the story. It begins to explore the process patterns for identifying microservices and events.
+ [Microservices](https://github.com/cdegroot/cloud-patterns-book/tree/master/Microservices/README.md) then brings in the set of patterns for implementing the microservices found by following the process patterns in the previous section
+ [Event Based Architecture](https://github.com/cdegroot/cloud-patterns-book/tree/master/Event-Based-Architecture/README.md) is the core set of patterns for building microservices that are oriented around event processing.
+ [Scalable Store](https://github.com/cdegroot/cloud-patterns-book/tree/master/Scalable-Store/README.md) contains the patterns for identifying the right persistence mechanism for a particular microservice implementation.
+ [Container Architecture](https://github.com/cdegroot/cloud-patterns-book/tree/master/container-architecture/README.md) contains the patterns around building a devops pipeline and managing the containers that your microservices will be deployed into.
+ [Cloud Native DevOps](https://github.com/cdegroot/cloud-patterns-book/tree/master/Cloud-Native-DevOps/README.md) continues the DevOps conversation by discussing many of the fundamental patterns around developing, testing and managing a cloud-native architecture.
