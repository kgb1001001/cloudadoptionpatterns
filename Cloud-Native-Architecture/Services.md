---
title: Services
parent: Cloud Native Architecture
---
Services
===

In most domains, some operations don't conceptually belong to any specific object. Previous design methods tried to force those operations into an entity-based model, often with adverse consequences, especially for operations that operated on a group of related Entities. 

**How do you model those aspects of a design that are not CRUD operations on an Entity or Aggregate?**

For instance, consider the simple case of modeling a transfer between Accounts.  It is fairly obvious that Transfer is not one of the CRUD operations of an account.  In fact, it seems to be its own unique thing.  So how do you represent these functional concepts that do not map to a specific Entity or Aggregate?

**Model those objects as stand-alone interfaces called Services.  Services can have their own REST interfaces.**

The rules for a good service are as follows:

* It is stateless
* The interface is defined in terms of other elements of your domain model (Entities, Aggregates and Value Objects)
* It refers to a domain concept that doesn't naturally correspond to any particular Entity or Value Object

These operations are part of the business domain—they're not technical issues of implementation. Things like "Login," "Authentication," and "Logging" aren't appropriate Services of this type. However, a concept like "Funds Transfer" in banking or "Adjudication" in insurance might be.

This pattern was first called out in [Daigneau](https://www.amazon.com/Service-Design-Patterns-Fundamental-Solutions/dp/032154420X)

