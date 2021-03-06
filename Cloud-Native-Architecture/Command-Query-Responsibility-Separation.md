# Command Query Responsibility Separation

You are building an application with a [Microservices Architecture](../Microservices/Microservices-Architeture.md).  You are determining your microservices through using the process of Domain Driven Design.  

**How do you manage the fact that your domain models for updates and reads may not be the same in a microservices environment?**

Therefore,

**Implement Command Query Responsibility Separation.  Build one microservice implementation that is based on the Command pattern that implements updates to the domain model and databases, and a separate implementation for queries**

In a very broad sense, this is an application of the [Bounded Context](Context.md) pattern.

![CQRS Implementation](../assets/CQRS.png)

CQRS was introduced to most people in [this paper](https://martinfowler.com/bliki/CQRS.html)
