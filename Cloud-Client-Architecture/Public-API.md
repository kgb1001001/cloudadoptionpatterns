---
title: Public API
parent: Cloud Client Architecture
---
Public API
===

You are building an application following the [Microservices architecture](../Microservices/Microservices-Architecture.md).  However, although you may be providing your own user interface, in the form of a web application, a mobile application or even a Chatbot, you also need to be able to enable third-party developers to use the services provided by your application.

**How do I best enable third party application developers to interact programmatically with my applications?**

A problem we have often encountered in Enterprises that need to work with third parties (business partners, governmental entities, etc.) is that they don't pay enough attention to the communication between what's inside their own walls and the entities.  There are two extremes in which we have seen companies fail in their public API approach:

1. The farthest end of the spectrum is assuming that you can simply publish your internal Microservices as API's to the world.  The result of this is that as these microservices change, that the changes are inflicted on the third parties outside of the company that depend on those API's.  This results in teams often having to support multiple versions of API (we have seen up to six supported at once!) because the third parties cannot change their code as fast as the internal development teams.

2. The other end of the spectrum is that the API's never change, resulting in lots of work, and lost opportunities inside the company itself.  For instance, many retailing companies still practice FTP file exchange with their suppliers for catalog entries, making it difficult to update catalog entries in real time, and forcing teams to write batch jobs to do daily or even weekly bulk updates.  As manufacturers become better at tailoring products for small market segments, this becomes untenable - especially as the number of products increases dramatically.

Neither end will work - both ends put an undue burden on one or the other partner, often both.  What is needed is something that moderates the changes and isolates internal changes to some degree from the external API.

Therefore,

**Build a separate, externally facing, microservice that implements a Public API. The service essentially operates as a facade to internal services.  This microservice will act as a specialized Backend for Frontend.**
