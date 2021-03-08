Cloud-native applications are those that are specifically written to run on the cloud, usually within a PaaS. They take advantage of the benefits of the cloud directly - for instance, using cloud functions like elastic scaling to meet capacity needs. What's more, these applications are built using different tools and runtimes than traditional applications.   They tend to be more likely to employ Polyglot Development and Polyglot Persistence. For example, an application might not use a relational database but instead use a NoSQL database, such as Cloudant or MongoDB.  Likewise, a Cloud-Centric application has a different set of assumptions about what is provided by its infrastructure and how.

Over the last several years that we have been building Cloud-Native applications we have found that there is a strong affinity between the [12 factors](http://www.12factor.net) and the Microservices Architecture. Microservices applications are automatically 12-factor compliant and thus more able to run in a Cloud-Native way. We have found that if you design for microservices and cloud native at the same time then the benefits to the team are multiplied.  Some of these benefits are:

* Faster development
* Smaller “Blast radius” for decisions
* Better ability to pick the right tool for the right job

In this section of our pattern language, we introduce some of the most basic patterns for Cloud-Native development.  These include:

+ [Microservice Design](Microservice-Design.md) is the root pattern of this section.  It leads you into a process of discovering your microservices through Domain-Driven and Event-Driven Design.
  + [Bounded Context](Context.md) is a key concept for developing a good microservice
  + [Identifying Entities and Aggregates](Identify-Entities-And-Aggregates.md) is required to identify all the microservices in a domain
  + [Identify Repositories](Identify-Repositories-And-Services.md) and [Services](Services.md) help you identify processing elements in your microservices
  + [Identify Domain Events](Identify-Domain-Events.md) is the final setp that helps you tie together the other pieces in your microservice design.
+ [Service Registry](../Cloud-Native-DevOps/Service-Registry-kyle.md) solves the problem of discovering services when your number of services increases and the complexity of dealing with local and remote services becomes difficult.
+ [Results Cache](Results-Cache.md) is a fundamental technique used to improve the performance of data access in a microservices design especially when microservices are being called repeatedly.
+ [Event Driven Architecture](../Event-Based-Architecture/Event-Driven-Architecture.md) is an important design consideration in building highly performant microservices architectures.
+ [Command Query Responsibility Separation](Command-Query-Responsibility-Separation.md) is a way of handling what happens when your database is separated into several different independent databases by microservices design.
