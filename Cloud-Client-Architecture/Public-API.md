---
title: Public API
parent: Cloud Client Architecture
---
Public API
===

You are building an application following the [Microservices architecture](../Microservices-Architecture.md).  However, although you may be providing your own user interface, in the form of a web application, a mobile application or even a Chatbot, you also need to be able to enable third-party developers to use the services provided by your application.

**How do I best enable third party application developers to interact programmatically with my applications?**



**Build a separate, externally facing, microservice that implements a Public API. The service essentially operates as a facade to internal services.  This microservice will act as a specialized Backend for Frontend.**
