---
parent: Cloud Native DevOps
title: Container per Service
---
# Container per Service

You are building an application with a [Microservices Architecture](../Microservices/Microservices-Architecture.md).  You want to use containers within a Container Platform like Kubernetes, or a Platform as a Service like Cloud Foundry.

**In a Microservices architecture, how do you distribute services across different containers?**

In a [Dr. Dobb's article](http://www.drdobbs.com/errant-architectures/184414966) (which was also incorporated into his book Patterns of Enterprise Application Architectures) Martin Fowler coined Fowler's First Law of Distributed Objects -- "Don't Distribute your Objects".  Wise words - ever since object Oriented Technologies became common, there was a tendency to try to set the boundary of Object distribution far too close to the metal as it were - a tendency to make every object in a systems design a distribution boundary.  As Fowler notes, the performance implications of this are legion - this is a step way too far in the distributed direction. 

However, the corresponding direction - "Never distribute your objects" is also a step too far.  One of the downfalls of early distributed object technologies like CORBA and EJB was that distribution at the object level fell entirely out of style.  Entirely self-contained monoliths - with the network boundary drawn entirely at the UI (e.g. HTML) level became far too common.  

Contributing to this was the coplexity of managing highly complex distribued systems.  Trying to deploy a distributed system was hard work, and one of the simplest ways of making that work easier was to build a self-contained monolith.  Part of what contributed to this work (and this perception that managing distributed systems was hard) was the time and effort it took to manage large farms of disparate VM's.

However, Containers are lighter weight than VM's.  Thus, many of the operational considerations that led you to want to minimize the numbers of VM's in your system (e.g. long startup time, long system stabilization times) do not apply in a conderized environment.

Despite this, containers are not a complete panacea.  With the lighter weight in terms of resource consumption and faster startup time comes a somewhat lower general availability.   Each individual container may have a lower uptime number than a corresponding VM.

Likewise, assuming that you would consider a container to be the equivalent of a thread is not necessarily the right approach either.  Containers do have a finite, even if small overhead.  And the startup, while very fast, is not instantaneous.

Therefore,

**Create a Container per Service. If necessary, to minimize runtime footprint, group Microservices vertically.**

Examples: See Building Microservices
