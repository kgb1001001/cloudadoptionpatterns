---
title: Results Cache
parent: Cloud Native Architecture
---
Results Cache
===

You are building clients for services, particularly in a Microservices Architecture. Making network calls to remote databases or services are expensive. Latency can be added by distance, layers or simply by long processing in a service.

**How do you improve the performance of your client application or microservice when it makes many repeated calls to services?**

-   Some services, when called repeatedly, return the same data every time and don’t cause any side effects. Example: A read-only database query.

-   Some services produce side effects. Example: A query that writes data or increments counters.

-   Caches can become very complex – especially if you try to anticipate what may need to be cached ahead of time.

-   Caching is optional. It should improve the performance of a system, but shouldn’t change behavior.

Therefore,

**Use a Results Cache that shortcuts the need to make repeated calls to the same service.**

Determining what to cache is often as difficult as setting up a cache itself. A common approach that is sometimes taken is to try to reproduce the data in a database locally to the application that is making requests of that data. The logic here is that if the problem is that database calls are expensive and slow, then by making those calls locally (perhaps in-memory) then you can reduce that overhead.

The problem is that if you simply reproduce the same data structures you have in a database locally to your program that you will have to also be able to reproduce the same type of operations on that data that your database is capable of making. The downside of that is that it's not easy or obvious to determine how to do the equivalent of a multi-way SQL JOIN statement together with database query optimization either in a language like Java or Node, or in a *Key-Value Store* like Redis!

Instead, consider using a Results Cache built from a simple [Key-Value Store](../Scalable-Store/Key-Value-Store.md) (either in-memory or in a [Scalable Store](../Scalable-Store/Scalable-Store.md)). For this to work, the cache client must be able to derive the key from the parameters of the database query or services call. Then the value is the last result returned from the service.

Probably the hardest issue to resolve in implementing a *Results Cache* is how to keep it from becoming stale. In many cases, the solution is simply to have a relatively low timeout value - in most interactive business applications it is relatively rare to have any cached data need a lifetime beyond that of a user session, which is usually measured in minutes -- so a short cache lifetime of a few minutes or less can significantly improve performance while still maintaining a minimal risk of the cache growing stale.
