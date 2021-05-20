---
parent: Scaleable Store
title: Columnar Store
---
Columnar Store
===

You are building an application that needs to store data in such a way that you can calculate statistics or perform aggregate queries from it.  This especially occurs in a [Microservices Architecture](../Microservices/Microservices-Architecture.md) when you are pulling data together from several microservices in order to perform queries or aggregate data.

**How do I store data when I'm often interested in a subset of the columns of all rows?**

Traditional [Table Stores](Table-Store.md) store data by row.  Thus, doing a query over any column will require you to do either a linear search, or to use an index to do a hashed search.  For most applications, that is fine - the tradeoff between being able to insert and update data quickly vs. a slight increase in query time is acceptable.  However, many types of analytics applications put a premium on query time, and do not require fast updates or inserts.  In this case, the row-oriented storage approach of a Table Store is not optimal.

Therefore,

**Use a Columnar Store that groups data by column, not by row. Column stores can very quickly operate on subsets of data as these subsets are stored close to each other.**

A major disadvantage of a Columnar Store is that updates and inserts may take longer than in other types of Scalable Stores.  They should also not be used when the data is loosely structured or unstructured - in a sense, you can think of a Columnar Store and a Table Store as being related in that they both perform best on highly structured data with a fixed, or very slowly changing schema.

Examples of Columnar Stores include Cassandra and Amazon RedShift. 
