Services
===

In most domains, some operations don't conceptually belong to any specific object. Previous design methods tried to force those operations into an entity-based model, often with adverse consequences, especially for operations that operated on a group of related Entities. Instead, you model those objects as stand-alone interfaces called Services. The rules for a good service are as follows:

* It is stateless
* The interface is defined in terms of other elements of your domain model (Entities, Aggregates and Value Objects)
* It refers to a domain concept that doesn't naturally correspond to any particular Entity or Value Object

These operations are part of the business domain—they're not technical issues of implementation. Things like "Login," "Authentication," and "Logging" aren't appropriate Services of this type. However, a concept like "Funds Transfer" in banking or "Adjudication" in insurance might be.

