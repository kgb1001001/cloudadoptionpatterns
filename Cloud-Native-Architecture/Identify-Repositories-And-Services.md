---
title: Identify Repositories
parent: Microservices Design
---
# Identify Repositories

You are building an application using a [Microservices Architecture](Microservices-Architecture.md).  You are working through the process of Domain Driven Design and you have discovered some terms in your vocabulary that don't seem to refer to either Entities or Aggregates.

**How do you handle concepts in your domain vocabulary that seem to refer to Sets of Entities?**

You want to enable searching of a Set of Entities (or Aggregates).  The problem is that searching for a specific set of Entities (or Aggregates) is not the same as querying a specific Entity or Aggregate.  A query that will bring back more than one Entity reference does not belong on the same REST interface as the query for the attributes of a specific Entity.  The two concepts are not the same.

Therefore,

**Introduce the concept of a Repository.  Separate the Repository API from the Entity or Aggregate API**

Here's the issue: Aggregates and non-aggregate Entities must be discovered through a search based on attributes. When you provide a search mechanism, you want to hide the details of the technical database infrastructure that implements search. The Repository is the thing that "maintains the illusion" that all objects are in-memory and instantly searchable while it hides the messiness of the database implementation behind it.

So a Repository becomes its own unique API (and possibly its own microservice, but not necessarily) that should be separated from the individual Entity or Aggregate API.


