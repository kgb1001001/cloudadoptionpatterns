---
parent: Scaleable Store
title: Polyglot Persistence
---
You are building applications using a [Microservices Architecture](../Microservices/Microservices-Architecture.md).

**How do you encourage teams to use the most optimized storage mechanism for the particular data structures, query and update requirements that each microservice requires?**

Teams building microservices are in an interesting and unusual position.  At one end, microservices themselves are about independence - independence to release new features on their own cadence, independence to change their internal implementation without affecting clients or requiring them to change, and independence to make their own decisions about clustering and HA.  

At the same time, teams are never entirely independent.  Even within a team, people want to follow common practices and standards in order to make their code understood and maintainable by other team members.  When a team is part of a larger organization, the desire to follow common practices and standards becomes even more important, as managers are concerned about the ability to supplement or replace team members that leave, become ill, or are otherwise unavailable.

The problem is that many organizations go too far in the commonality direction, especially as regards persistence.  Traditional development approaches often featured a shared data repository, usually a relational database.  Once a team heads down that path, it becomes difficult to leave, as the investment in terms of skills, licenses, management and especially the data itself grows every larger.

But microservices offer a different option.  Just as moving from a monolith to separate microservices allow teams to focus only on the specific business problem that each microservice is designed to solve when working with that microservice, the same principle of tighter focus allows teams to think more closely about the management and representation of the data they are persisting. 

Therefore,

**Apply Polyglot Persistence.  Let each team choose their own persistence mechanism (perhaps from a pre-selected set) that is appropriate to their particular business problem and implementation challenges.** 

Not every problem is suited to the same type of persistence mechanism.  Documents are not searchable when they are stored in Key-Value stores.  Relational Databases are not particularly well suited to the problem of storing unstructured or loosely-structured data.  Polyglot Persistence addresses this problem and allows teams to make their own decisions.

However, Polyglot persistence does not solve all problems - it creates a few new ones as well.  In particular, especially when in a refactoring situation applying the [Strangler Pattern](../Cloud-Adoption/Strangler-App.md) you may find that synchronizing your data between different types of store becomes more challenging.  In cases like this you may need to employ an Event-based solution using an [Event Backbone](../Event-Based-Architecture/Event-Backbone.md) or a [Data Virtualization](../Coexistence-Patterns/Data-Virtualization.md) approach that makes non-relational stores look like relational stores to external clients. 
