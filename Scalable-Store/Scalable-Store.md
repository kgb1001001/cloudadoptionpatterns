# Scalable Store

You are developing an application using [Business Microservices](../Microservices/Business-Microservice.md). However, your application will need persistent state to represent current and previous user interaction.

**How do you represent persistent state in an application?**

-   Storing application data inside the memory of an application runtime leads you to require routing solutions like sticky sessions that make building highly available systems difficult.

-   You don’t want to limit the scaling of your application by forcing the application to store state inside a data store that cannot scale linearly.

**Put all state in a Scalable Store where it can be available to and shared by any number of application runtimes.**

The key here is that the database must be naturally distributed and able both to scale horizontally and to survive the failure of a database node. For the last several years, that has driven developers to the concept of “NoSQL” databases as described in \[Sadalage\]. Examples of this type of database include Redis, Cloudant, Memcached.

However, quite recently a number of new distributed databases based on the relational model and collectively called “NewSQL” have also become available. These include options like Clustrix, MemSQL, or even MySQL cluster. NoSQL databases are typically less efficient at SQL-like queries because of differences in approaches to query optimization. So, if your application depends on SQL-centric complex query capability then a solution such as a NewSQL database or a distributed in-memory SQL database may be more efficient.

In the end it does not matter which particular database you choose – so long as you choose the right database structure and retrieval mechanism for the job you are trying to perform. If the driving forces in your application are scalability and redundancy either a NoSQL or NewSQL database would suffice, but other application requirements will determine the particular type of database you must choose.

[Result Caches](../Cloud-Native-Architecture/Result-Cache.md) and [Page Caches](../Cloud-Native-Architecture/Page-Cache.md) are usually implemented with a *Scalable Store*.

If your Scalable Store does not fully implement Synchronization across multiple Datacenters (e.g. [Three Datacenters](Three-Data-Centers.md)) you may need to implement [Global Locking](Global-Locking.md).
