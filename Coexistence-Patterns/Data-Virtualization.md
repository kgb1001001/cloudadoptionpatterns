---
parent: Coexistence Patterns
title: Data Virtualization
---
# Data Virtualization

You are building a [Microservices Architecture](../Microservices/Microservices-Architecture.md) and you are refactoring applications to Microservices using an approach like the [Strangler Application](../Cloud-Adoption/Strangler-App.md) to pull out microservices a few at a time on a domain by domain basis.  You are in a situation where it is easier to refactor the business logic first before you refactor the data, but you need to be able to plan out a path for refactoring the data.

**How do you allow your microservices code to act as if each owns its own data while in the transition period before the data is fully refactored?**

Refactoring is always challenging in a brownfield environment, and is even more so when a large application has a correspondingly large and complex database that is shared by many parts of the application or (even worse) many separate applications.  In many cases where multiple teams are involved, it is often easier to start with refactoring code (which may be owned by an application team) than it is data (which may be shared among several teams or owned by separate Data team).  In that case, you still need to be able to make it seem to each Microservice that they are independent, even though for a time they are not.  You want to let each Microservice determine its own unique schema and database queries and updates, while at the same time letting the underlying data remain unchanged for the remainder of the monolithic application that has not yet been refactored.

Therefore,

**Employ a Data Virtualization strategy that separates the underlying data representation from the data representation exposed to the application.**

Data Virtualization as an approach can be implemented in many different ways.  There are a multitude of commercial products that implement Data Virtualization over several open source and commercial databases.  This includes the [IBM Cloud Pak for Data](https://www.ibm.com/analytics/data-virtualization) and the [IBM Virtualization Manager for z/OS](https://www.ibm.com/products/data-virtualization-manager-for-zos) that also covers traditional mainframe databases and file formats, in addition to products like [Data Virtuality](https://datavirtuality.com/) and [Informatica](https://informatica.com) that cover a wide range of data options.  

If you are working on a Relational Database, perhaps the simplest Data Virtualization approach is just to begin with building Views in your database either Materialized or Standard, which can give you multiple different viewpoints on the same underlying data.  Sam Newman covers this as a pattern in his [book](https://samnewman.io/books/monolith-to-microservices/) but the downside of this is that even though this gives you freedom to use the new queries in your code, it is limited to originating relational databases only. If your originating database is not relational (e.g. is a flat file or other legacy database format) you can't build a view from it and must instead use a Data Virtualization tool. 
