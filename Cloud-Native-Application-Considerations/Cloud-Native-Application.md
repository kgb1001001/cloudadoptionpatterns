---
parent: Cloud Native Application Considerations
title: Cloud-Native Application
---
# Cloud-Native Application

**How can I architect an application to take maximum advantage of the cloud platform it will run on?**

**Architect the application as a *cloud-native application* by implementing the custom business logic in an application separate from the reusable backend services.**

The application runs in an [Application Runtime](Application-Runtime.md), has an [Application API](Application-API.md), and is a [Stateless Application](Stateless-Application.md). Each application connects to multiple (zero or more) backend services, where each is a [Backend Service](Backend-Service.md).

