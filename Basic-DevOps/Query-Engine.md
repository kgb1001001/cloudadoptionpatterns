---
parent: Basic DevOps
title: Query Engine
---
# Query Engine

You are building a system made up of many cooperating services, some of which you have created on your own with a Microservices Architecture, some of which may be obtained from third parties or a cloud provider.  

**How do you view all of the different log entries that each service produces and make sense out of the structure of what is being logged?  How can you extract information from all of the data in these log entries?**

You need to be able to create searches that can (for instance) correlate the set of calls that start with a single user request.  

Therefore,

**Use a query engine to treat the set of logs as a database.  Formulate queries that allow you to extract related log entries and make sense out of call graphs that cross multiple service boundaries.**

The combination of LogStash (which acts as a [Log Aggregator](Log-Aggregator.md) to collect and transform log entries) and ElasticSearch (which allows full-text search of the collected entries) is often cited as the most common way to make sense out of the distributed logs created by a Microservices design. 
