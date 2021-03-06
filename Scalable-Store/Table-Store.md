Table Store
===

You are building a cloud-native application, particularly one following the [Microservices Architecture](../Microservices/Microservices-Architecture.md).  You may be either creating a new, greenfield application or following [Cloud Refactoring](../Cloud-Adoption/Cloud-Refactoring.md) principles to refactor an existing application.

**How do I represent data that is going to be queried arbitrarily?**

Some applications go beyond basic "CRUD" operations in that they require the ability to arbitrarily query on data.  This is particularly true of applications that have a reporting element, especially in cases where the reports change frequently.

Likewise many existing applications are already using a table format for their data.  If the level of pain caused by ORM is low (for instance, the application is a standard CRUD application and is using a simple ORM like Hibernate) then there is no pressing reason to force a different data representation.

However, on the other hand, there are many applications in which the level of pain caused by ORM is "high".  In those cases, the downsides of the table model may outweigh the benefits.  In these cases, the only reason that teams often choose a relational databases are because of technology inertia (e.g. it's what they know) or corporate or organizational guidelines.

Therefore,

**Choose a "classical" RDBMS when the data is naturally table-oriented, most columns are usually needed for operations, and the data has a heavy use of inter-table relations.**

There are literally dozens of examples of relational stores, running from classical databases like Oracle and DB2 to more recent open-source systems like MySQL and PostgresDB.
