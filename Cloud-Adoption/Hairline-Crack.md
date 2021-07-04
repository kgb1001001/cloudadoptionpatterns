---
title: Hairline Crack
parent: Cloud Adoption
---
# Hairline Crack (aka Fracture Plane)

You are evaluating an existing application for cloud adoption.  You know you want to take some or all of the functionality of the application and re-architect it for microservices in order to improve the maintenance of the application and to reduce the blast radius of new changes to the application.

But how do we migrate a monolith into a collection of services? It's not easy to understand all at once how a monolithic application can be broken apart into microservices. 

**How do you find a way to identify the areas within an application that might be amenable to refactoring into a microservice?** 

What you must look for are the places where the pieces of a monolith that will be easy to "force apart".  This is usually indicated by the presence of an existing API to the outside world - if an application has multiple API's that it exposes then there are often good odds that one or more of them can be split apart from the others.

Therefore,

**Look for Hairline Cracks - these are the places where the monolith will be easy to break.**

The places where a monolith can be forced apart most easily are those places in the application where there are already some sort of interface between sections of the monolith.  This is analogous to a hairline crack in a piece of metal or a Fracture plane in some rocks.  In large monolithic Java applications, there are at least three very simple cases where you can find obvious cracks that can be exploited regarding services.  These three cases are:

Case 1: Existing REST or JMS services – This is by far the easiest case for refactoring.  It may be that you have existing services that are already compatible with a Microservices architecture, or that could be made compatible. Start by untangling each REST or simple JMS service from the rest of the WAR and then deploy each service independently.  At this level duplication of supporting JAR files is fine – this is still mostly a question of packaging.  Here you have begun the process by splitting things off into what may be called a "Macroservice", but remember that this is just a step toward a refactoring into Microservices.  Your application will still need to not only follow the principle of doing one and only one business function, but also you will need to make sure you're following accepted [Cloud DevOps](../Cloud-Native-DevOps/Cloud-Native-DevOps.md) principles.

Case 2: Existing SOAP or EJB services – If you have existing services, they were probably built following a functional approach (such as the Service Façade pattern).  In this case, functionally based services design can usually be refactored into an asset-based services design.  This is because in many cases, the functions in the Service façade were originally written as CRUD operations on a single object.   In the case where that is true, the mapping to a RESTful interface is simple – just re-implement the EJB session bean interface or JAX-WS interface as a JAX-WS interface – you may need to convert object representations to JSON in order to do this, but that’s usually not very difficult, especially where you were already using JAX-B for serializations.   In cases where it’s not a simple set of CRUD operations (for instance account transfer) then you can apply a number of different approaches for constructing RESTful services (such as building simple functional services like /accounts/transfer) that implement variants of the Command pattern.

Case 3: Simple Servlet/JSP interfaces.  Many Java programs are really just simple Servlet/JSP front-ends to database tables. They may not have what is referred to as a “Domain Object” Layer at all, especially if they follow design patterns like the Active Record pattern.  In this case, creating a domain layer that you can then represent as a RESTful service is a good first step.   Identifying your domain objects by applying Domain Driven Design will help you identify your missing domain services layer.  Once you’ve built that (and packaged each new service in its own WAR) then you can either refactor your existing Servlet/JSP app to use the new service or you can build a whole new interface following the [Multichannel Architecture](../Cloud-Client-Architecture/Multichannel-Architecture.md) approach.

In any of these cases, what you want to do is then to apply [Microservice Design](../Cloud-Native-Architecture/Microservice-Design.md) in order to determine what design you want to refactor toward.

