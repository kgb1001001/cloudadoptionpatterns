Microservices DevOps
===

You are building a complex application with a [Microservices Architecture](../Microservices/Microservices-Architecture.md). You need to be able to put that system into production.

**How do you balance the needs of developers (which want to work on small, easy-to-modify artifacts) and operations teams, which need to minimize the impact of changes on critical systems in order to maintain availability?**

-   If you deploy microservices in the same way you deployed a monolithic application, you will not obtain the benefits of a microservices architecture.

-   If you let each team go off and follow their own approach without setting guidelines on how microservices are deployed, modified and managed, it will be impossible to debug the resulting system.

Therefore,

**Follow a *Microservices DevOps* approach that allows you to isolate each Microservice as much as possible, while being able to easily and quickly identify and resolve issues with the Microservices. This begins with the fundamental principle of deploying one [Container Per Service](Container-Per-Service.md)  Applying unique [CI/CD pipelines](CD-Pipeline.md) to each Microservice will allow you to build and deploy each microservice individually. However, having shared, common deployment and operations approaches allows you to set guidelines on how microservices interrelate and interact with each other**

Since changes to a microservice can occur at any time, other microservices need to be isolated from the results of that change through a *Services Registry*.

What’s more, microservices cannot function completely independently – since each microservice will depend on other microservices or other downstream services (such as a [Scalable Store](../Scalable-Store/Scalable-Store.md)) you need to apply techniques such as a [Log Aggregator](Log-Aggregator.md) and [Correlation ID’s](Correlation-ID.md) to understand the interaction between different microservices and debug issues.
