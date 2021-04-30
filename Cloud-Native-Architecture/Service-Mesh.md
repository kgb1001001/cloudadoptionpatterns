---
title: Service Mesh
parent: Cloud Native Architecture
---
# Service Mesh

You are building an application following a Microservices Architecture.

**How do you ensure that the different services in your design can securely communicate with each other, and also make sure that such communication is optimized for the topology of your overall system?**

The problem with Microservices is that there are so many of them!  In the monolithic world, everything resides in the same process - communication between components is in memory, and static typing and linking prevents you from trying to "fall off" the end of the process and call something that is not available.  The issue is that with Microservices this is no longer true.  With a Microservices design, not only can microservices processes be either present or entirely absent (because processes can crash) but there can be multiple instances of each microservice!  Even performance management becomes more challenging to implement, because instead of calls that are fixed in time, you have the vagaraties of network communication added into the mix.  

You need help to work through these issues.  You need to know how to send requests that will be carried out, regardless of the physical location of the service, or which instance of the service handles it, and you also need to make sure that if there are problems or slowdowns that they can be identified and dealt with before they become an issue.

Therefore,

**Use a Service Mesh to link your services together.**

A Service Mesh is configurable infrastructure layer that is designed to handle interprocess communication between different services.  It makes sure that the communication between services is fast, reliable and secure.  Most Service meshes not only implement traffic management, load balancing, policies and access management but also implement the [Circuit Breaker](../Microservices/Circuit-Breaker.md) pattern as well to deal with issues in communication and scaling. 

[Istio](https://istio.io/) is one example of a completely open source service mesh that works transparently between existing microservices.  It includes APIs to let it integrate into logging, telemetry and policy systems.  Istio uses a Sidecar approach in which an Istio Sidecar runs in the same container as your microservice allowing it to intercept network calls and add additional features such as Circuit Breakers.

In most cases you would need to combine a Service Mesh together with a [Services Registry](../Cloud-Native-DevOps/Service-Registry-kyle.md)
