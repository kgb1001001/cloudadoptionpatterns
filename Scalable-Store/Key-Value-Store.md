---
parent: Scaleable Store
title: Key-value Store
---
# Key Value Store

You are building an application with a [Microservices Architecture](../Microservices/Microservices-Architecture.md).

**How do you store data that is naturally accessed through a
simple key lookup such as cache entries?**

-   You want to use the simplest tool for the job at hand.

-   You want to make your accesses (Cache lookups or other accesses) as
    fast as possible.

**Store your data in a scalable Key-Value Store. The
principal advantage of a key value store over other types of Distributed
Store is its simplicity. Most Key-Value Stores act, in principle, like a
hash map.** 

For example, Redis has simple GET and SET commands to store
and retrieve string values. What’s more, for simple key lookup
operations, Redis offers O(1) performance.

If, on the other hand, you used a more complex store type such as a
[Document Store](Document-Store.md) for storing cache entries, then you would find that the
performance of such solutions is often not as good. That is because
other distributed store types optimize for more complex cases such as
searching by the contents of the documents stored.

There is no magic in using a Key-Value store. In many cases such as
EhCache, they are in-memory stores, and as such only can provide
Consistency and Availability but not Partition tolerance (as per
Brewer’s CAP Theorem). This limits the size of the cache. The mechanism
used by many others (e.g. Redis with clusters) is to map keys to
specific distributed nodes, and to route requests to the appropriate
server, which then stores that corresponding set of values in memory. In
order to maintain Availability, this means that you must have copies
(slaves) of each node. This means that by the CAP theorem you can gain
Partition tolerance, but at the potential loss of Consistency while the
master synchronizes with the slave.
