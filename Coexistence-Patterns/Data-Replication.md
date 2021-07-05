---
parent: Coexistence Patterns
title: Data Replication
---
# Data Replication

You are following a [Cloud Refactoring](../Cloud-Adoption/Cloud-Refactoring.md) strategy using the [Strangler Application](../Cloud-Adoption/Strangler-App.md) and you find the need to slowly refactor a database over time so that each [Domain Microservice](../Microservices/Business-Microservice.md) can in the end own its own data.  However, since this process may take months or even years, you will find yourself in the situation where you have different clients that are querying and updating the data in the original, monolithic database, and also the data in the individual distributed databases for each microservice.

**How do you keep the data synchronized between the two different sets of databases?**

The problem with trying to keep two different databases (especially those that are implemented in different technologies) is that you loose some of the ease of development that happens when you are using a single, monolithic database.  Some of these issues are in development only (such as the fact you may have two different programming models for accessing and updating the databases) but many of them are operational as well.  The fact that the two databases may be from different vendors, or even implemented with different technologies (such as an Oracle database being replaced by a Cassandra database) means that the job of keeping the applications that use them in sync becomes more complex.  

Therefore,

**Employ a Data Replication approach that updates both sets of databases whenever one changes.**

Data Replication is a strategy that can work in a couple of different approaches, but which approach you choose depends on the particular situation you find yourself in.  In situations where data cannot ever be different between the two databases, a [Synchronous Replication](../Scalable-Store/Sync-Replication.md) approach is often the best.  However, all Synchronous replication approaches share the same drawback - they increase the time it takes to finish any update transaction on either database, since you have to wait until you receive confirmation of the update on the target database before the transaction can complete on the original database.  What's more, most synchronous approaches are going to be technology-specific, that is, you will have to choose a replication tool that supports your particular database.  So, for instance, if you want to replicate part of an Oracle database to another Oracle database,  you would use Oracle GoldenGate to provide real-time synchronous replication. 

[Asynchronous replication](/Scalable-Store/Async-Replication.md) schemes have the advantage that they can be more flexible in how you manage the data transformation between the origin and target database.  For instance, Change Data Capture approaches that connect to Kafka allow you to route the change logs (often expressed as Events) from the origin to to multiple different receivers that could transform that data into their own target format.
