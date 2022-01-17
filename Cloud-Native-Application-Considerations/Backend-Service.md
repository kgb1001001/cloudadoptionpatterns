---
parent: Cloud Native Application Considerations
title: Backend Service
---
# Backend Service

You are developing an application architected as a [Cloud-Native Application](Cloud-Native-Application.md). The application implements custom business logic and is a [Stateless Application](Stateless-Application.md).

**How can multiple applications share the same reusable functionality?**

This functionality can be specialized and designed to be as reusable as possible, whereas the application is customized for specific user requirements.

If the application is stateless, where is the state stored?

If the reusable functionality is multitenant, multiple applications can share it.

**The application binds to the reusable functionality as a *backend service*. The service can be stateful and can be reused by multiple applications.**

Many cloud platforms provide multiple backend services, available for applications deployed on that platform to use.

"A backing service is any service the app consumes over the network as part of its normal operation. ... Backing services like the database are traditionally managed by the same systems administrators who deploy the app’s runtime. In addition to these locally-managed services, the app may also have services provided and managed by third parties." [The Twelve-Factor App: IV. Backing services](https://12factor.net/backing-services)
