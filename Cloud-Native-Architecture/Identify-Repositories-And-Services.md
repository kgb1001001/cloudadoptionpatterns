# Identify Repositories

You are building an application using a [Microservices Architecture](Microservices-Architecture.md).  You are working through the process of Domain Driven Design and you have discovered some terms in your vocabulary that don't seem to refer to either Entities or Aggregates.

**How do you handle concepts in your domain vocabulary that seem to refer to Sets of Entities?**

You want to enable searching of a Set of Entities (or Aggregates).

**Introduce the concept of a Repository**

Here's the issue: Aggregates and non-aggregate Entities must be discovered through a search based on attributes. When you provide a search mechanism, you want to hide the details of the technical database infrastructure that implements search. The Repository is the thing that "maintains the illusion" that all objects are in-memory and instantly searchable while it hides the messiness of the database implementation behind it.


