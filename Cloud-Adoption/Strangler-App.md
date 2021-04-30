---
title: Strangler Application
parent: Cloud Adoption
---
# Strangler Application

You are starting with a legacy monolith that is implemented as a Web application.  When migrating legacy applications to the cloud you often need to consider how to replace the application in a piecemeal way.  Often, a legacy monolith does not show obvious Hairline Cracks. How can we replace it with a [Microservices Architecture](../Microservices/Microservices-Architecture.md) without doing a full rewrite?  A full all-at-once rewrite and replace is a risky operation and would also be expensive and would not show value until the complete rewrite is finished.  

**You need an approach that allows you to avoid a full "big-bang" rewrite and replace, yet still allows you eventually replace the entire monolith.**

Therefore,

**Use the structure of the web application and HTTP to redirect requests for parts of the application away from the legacy monolith and towards a new implementation of those features.  Add features incrementally to the new application (the strangler application) and update the redirection logic towards the new features as they are added.**

An important consideration when applying the Strangler Application is that you have to consider that there is a difference between the release management of an entire application and the release management of an individual microservice.  The concept that has become most important for teams adopting this process is the concept of a Chunk. Chunks that are groups of Microservices and associated user interface components that are tied together either by implementation restrictions or User-Experience relationships that become initial large-scale release units.

Identifying a chunk is done by comparing the existing functionality of the application with the desired functionality of the application while you specifically focus on the user interface flows that the new microservices will change or interrupt.  For example, consider that you have a retailing website implemented as a monolith built using page-at-a-time templating technologies that you want to refactor into microservices.  A retail website has several common aspects - you want to be able to browse a catalog, search for items, add items to a shopping cart, and check out.  Some of these elements, like item search, are relatively self-contained and so would make good first choices for refactoring into microservices.  However, if we consider a more complicated aspect of the website like checkout you can see that it may contain multiple different aspects to a user interface flow - you want to verify availability of items, show tax calculations, obtain shipping information, and obtain payment information.  Each of these aspects individually may make good microservices.  But you can't very easily split them apart from the other parts of the checkout flow.  

So you may rebuild the checkout process as a new [Single Page Application](../Cloud-Client-Architecture/Single-Page-Application.md), that then calls down through one or more [BFF's](../Microservices/Backend-For-Frontend.md) into [Business microservices](../Microservices/Business-Microservice.md) for Inventory, Tax, Shipping and Payment. But for the initial release, the entire Checkout process must be updated at once, or the resulting flow could be jarring to the user as they flip back and forth between two different user experiences.  After the initial release, each individual microservice could then be updated separately from the rest as the individual delivery pipelines can be independently managed.

Reference: Martin Fowler's [Strangler Application](http://www.martinfowler.com/bliki/StranglerApplication.html)
