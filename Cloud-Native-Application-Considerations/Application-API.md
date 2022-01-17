---
parent: Cloud Native Application Considerations
title: Application API
---
# Application API

You are developing an application architected as a [Cloud-Native Application](Cloud-Native-Application.md).

**How should the application expose itself to clients who want to use the application?**

Sockets? CORBA? EJBs? Database integration? Messaging queues?

APIs make applications easier to work with, separating interface from implementation, acting as a contract between the consumer and provider.

The Web (HTTP) is the universal network.

The first Web API was SOAP and the WS-* standards for web services. REST became more popular.

**The application should publish an *application API* used to access its functionality and implement that API. It should bind itself to an HTTP port and listen for client commands that conform to that API.**

The API should be RESTful (at least until another standard replaces REST the way REST replaced SOAP).

"The web app exports HTTP as a service by binding to a port, and listening to requests coming in on that port. ... the port-binding approach means that one app can become the backing service for another app, by providing the URL to the backing app as a resource handle in the config for the consuming app." [The Twelve-Factor App: VII. Port binding](https://12factor.net/port-binding)
