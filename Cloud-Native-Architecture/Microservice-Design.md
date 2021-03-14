# Microservice Design

You are embarking on developing an application using a *Microservices Architecture*. You understand the benefits of using microservices for new applications and refactoring applications to microservices, but you are usure how to start.

**How do you design the microservices that your application needs? What are the elements of a good microservices design?** 

The answers lie in some of the basic premises of object-oriented programming. The book Domain-Driven Design: Tackling Complexity in the Heart of Software (Evans 2004) captures a meta-process for designing software that object-oriented software development teams have used for years. The book isn't about specific design notations or even specific classes of objects or patterns. Instead, it covers the general categories of objects that good object-oriented designers identify and work with. Those categories become critical elements of a good microservices design.

*Therefore,*

**Follow a Domain Driven Design  and Event Driven Design Approach for identifying Microservices**

* Understand the [Bounded Context](Context.md) for this subdomain
* Start with [Identifying Entities and Aggregates](Identify-Entities-And-Aggregates.md)
* Next [Identify Repositories](Identify-Repositories-And-Services.md) and [Services](Services.md)
* Finally [Identify Domain Events](Identify-Domain-Events.md)

*Putting it all together*

When you follow the Domain-Driven Design process, you end up with these object types:

* A list of Entities, some of which are Aggregates, including identified root Aggregates and Entities
* A set of Repositories
* A list of Value Objects that are associated with one or more Entities
* A list of Services that correspond to functions that aren't part of any particular Entity
* A list of Domain Events that connect the Entities, Aggregates and Services together

In summary, when you design microservices for an application, use the principles of Domain-Driven Design to guide you along the way. Establish the Bounded Context for your team and list your Entities, Repositories, Value Objects, Services and Domain Events within the Bounded Context. Then, use what you learned to define and design your microservices.

These object types are what you need to create your first-pass RESTful service design for microservices. Not all of these objects become part of your microservices design—some might be hidden in your service implementation—but you can start to understand the objects that you're dealing with.

See [Sidebar - Which Comes First API's or Entities?](Sidebar-API-Entity.md)

Once you  have decided to embark on a Microservices Design approach, you will next need to consider your DevOps Approach.  Old methods of development and deployment will not suffice in a microservices world.  You'll need to look at a [Cloud Native DevOps](../Cloud-Native-DevOps/Cloud-Native-DevOps.md).
