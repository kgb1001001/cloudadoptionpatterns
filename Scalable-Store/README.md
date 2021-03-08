# Scalable Store Introduction

A key part of the microservices architecture is that wherever possible each microservice should control or “own” its own data.  However, microservices are also expected to be scalable and stateless.  This combination of requirements leads to the need for Scalable Stores, which is the root pattern of this section.  

+ [Scalable Store](Scalable-Store.md) addresses how to avoid scalability bottlenecks in a microservices architecture by using databases that are naturally distributed and able both to scale horizontally and to survive the failure of any database node.
+ [Key-Value Store](Key-Value-Store.md) allows you to do simple lookups by acting in principle, like a hash map, with accompanying O(1) performance for many use cases.
+ [Document Store](Document-Store.md) allows you to store native schemaless JSON data in a database optimized for storing that type of information.
+ [Table Store](Table-Store.md) recognizes the fact that relational representations are still sometimes the right way to store and manage certain types of application data.
+ [Polyglot Persistence](Polyglot-Persistence.md) is critical in helping grant teams building microservices the independence to choose the right tool for the job.

Certain architectural concepts are critical to understanding how Scalable Stores scale across multiple datacenters.

+ [Synchronous Replication](Sync-Replication.md) is the solution for when data cannot be lost at all, at any time and must be constantly consistent.
+ [Asynchronous Replication](Async-Replication.md) is the solution for other cases - when data should not be lost but may be inconsistent over a period of time.
+ [Global Locks](Global-Locks.md) are required when implementing systems that require consistency of data across multiple datacenters.
