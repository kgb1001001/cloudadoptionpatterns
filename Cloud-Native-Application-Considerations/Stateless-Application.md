---
parent: Cloud Native Application Considerations
title: Stateless Application
---
# Stateless Application

You are developing an application architected as a [Cloud-Native Application](Cloud-Native-Application.md) with an [Application API](Application-API.md).

**How can the application simplify scalability, such that the cloud platform can easily manage the application's capacity?**

Vertical scaling is limited by a computer's capacity. The application runs as a process, so capacity can be added by running more processes. Horizontal scaling runs more processes, which can be multiple on one computer or distributed across multiple computers.

A load balancer distributes client requests across processes. The processes might as well be the same size since they will receive the same number of requests, so vertical scaling doesn't help much. Each process should have the same state so that any requests can be sent to any process. Either the state of the processes needs to be synchronized or, better yet, the processes should have no state. With stateless processes, there's no state to manage and any process can handle any request.

**Make the application a *stateless application*. The process' memory space can be used as a brief, single-transaction cache. The application loads the data it needs from domain databases running in backend services and updates the data in those services. Session state used across transactions must be stored in a backend service such as an in-memory database. All processes running the application share the same set of backend services and therefore the same set of session and domain data.**

Each call to the application API defines a transaction. The service can cache data during the transaction but not between transactions. The application writes any data that needs to be saved from a transaction to the [Backend Services](Backend-Service.md), such as databases.

When the application scales out by starting new processes, the new ones are just like the existing ones because they're all stateless. When the application scales in by stopping some of the processes, any of them can be stopped because they're all equivalent. Because they're stateless, stopping the process is easy and will not corrupt the data.

The load balancer does not need to support sticky sessions to send requests from the same client to the same process. Since the processes are stateless, each request can be served equally well by any process.

"Twelve-factor processes are stateless and share-nothing. Any data that needs to persist must be stored in a stateful backing service, typically a database. The memory space or filesystem of the process can be used as a brief, single-transaction cache. ... Sticky sessions are a violation of twelve-factor and should never be used or relied upon. Session state data is a good candidate for a datastore that offers time-expiration, such as Memcached or Redis." [The Twelve-Factor App: VI. Processes](https://12factor.net/processes)

"[Each application runs in its own application runtime process.] "the application must also be able to span multiple processes running on multiple physical machines." The process model truly shines when it comes time to scale out. The share-nothing, horizontally partitionable nature of twelve-factor app processes means that adding more concurrency is a simple and reliable operation." An individual process can handle its own internal multiplexing, via threads inside the runtime, can support the async/evented model, and vertical scaling is possible. [The Twelve-Factor App: VIII. Concurrency](https://12factor.net/concurrency)

"The twelve-factor app’s processes are disposable, meaning they can be started or stopped at a moment’s notice. This facilitates fast elastic scaling, rapid deployment of code or config changes, and robustness of production deploys." [The Twelve-Factor App: IX. Disposability](https://12factor.net/disposability)
