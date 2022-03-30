---
parent: Basic DevOps
title: Correlation ID
---
Correlation ID
===

You are building an application in a [Microservices Architecture](../Microservices/Microservices-Architecture.md). Your application may use [Backends for Frontends]((../Microservices/Backend-For-Frontend.md)) and multiple [Business Microservices](../Microservices/Business-Microservice.md) and [Adapter Microservices]((../Microservices/Legacy-Adapter-Microservice.md)), and may have complex call graphs as a result.

Building Microservices is the easy part.  Operating Microservices, and debugging problems when they occur is the more challenging aspect.  By multiplying the number of processes in your overall system (which happens when adopting a Microservices Architecture) you increase the overall operational complexity by increasing the number of discrete processes, and thus different logs with different entries, that may be created.  The result is that instead of a call graph being abl to be debugged by simply comparing timestamps in a simple log, a single business transaction may consist of a more complex web of calls moving in and out of several disparate processes.

**How do you debug a complex call graph when you do not know where in the set of microservices along that call graph the problem may have been introduced?**

-   You don’t want to overly burden your developers with complex requirements for logging and monitoring

-   You need to be able to trace a call regardless of how complex or simple that call is.

Therefore,

**Consistently use Correlation ID's to tie multiple microservice calls together. A correlation ID is a simple identifier (usually just a number) that is passed in to every service request and passed along on every succeeding request – when any service logs something for any reason, the correlation id is printed in the log entry. This allows you to match or correlate specific requests to one service to other service requests in the same call chain.**

Implementing correlation id’s correctly requires four consistent actions:

1.  Create correlation ID if none exists and attach it as a header to every outgoing Service Request

2.  Capture the incoming correlation ID on every incoming request and log it immediately

3.  Attach the correlation ID to the processing of the request (perhaps using a threadlocal variable…) and make sure that the same correlation ID is passed on to any downstream requests

4.  Log the correlation id and timestamp of \*any\* messages that are connected to that thread of processing

Once you have implemented a *Correlation ID* you can then use a [Log Aggregator](Log-Aggregator.md) to gather together all of the logs across all of the dependent systems in your [Microservices Architecture](../Microservices/Microservices-Architecture.md) and can perform a query for the *Correlation ID* against the aggregated log. When placed into timestamp order the results of this query will show the call graph of the solution and allow you to put errors into the appropriate context in terms of which microservice instance and thread handled the calls, and what the parameters to the calls were at the time that the problem was encountered.

Correlation ID was originally called out in [Hohpe](https://www.amazon.com/Enterprise-Integration-Patterns-Designing-Deploying/dp/0321200683)
