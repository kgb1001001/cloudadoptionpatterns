---
title: Interaction Model
 	(aka Application Model)
parent: Cloud Client Architecture
---
# Interaction Model (aka Application Model)
  
You are building an application (or application suite) in a Multimodal Architecture that needs to interact with the user on multiple technology platforms, such as a Mobile application, a Web Site, or through a Social Media platform. 

**How do you avoid mixing business and UI logic and duplicating effort and code when you are building a Multimodal Architecture?**

Mixed business logic and user interface logic is the bane of many corporate developer’s existence.  Unfortunately, it is more common than not.  This is one reason why “refactoring the monolith” has become so popular – often little attention was paid to the separation of UI and business logic, resulting in business logic that is spread throughout different layers of a system, and that is inconsistent in its handling of user input and requests, sometimes leading to security issues.

What’s more, in a [Multimodal Architecture](Multimodal-Architecture.md), there are concepts that span multiple different technology platforms.  The concept of a User is something that exists regardless of whether the user is interacting with a system through a web application or through a mobile application.  Allowing the user to carry their “identity” through the different channels is important to the user in order to follow the principle of “least astonishment”, but also is vitally important in debugging problems where users may find different results for the same interaction on different platforms.   This also leads to the need for consistent logging in order to ensure that these complex multimodal systems can be debugged.

Therefore,

**Explicitly create components that model the interaction with the user.  An Interaction Model captures a particular form of user interaction on a particular channel or technology stack.** 

The primary reason for the Interaction Model is to separate the domain logic from the user interface logic.  That also separates the channel-specific libraries such as those for mobile applications on iOS, or browser-based applications in React from the rest of the application as well.  Thus, the Interaction Model will interface with both these libraries and the back end microservices model (either through a [Backend for Frontend](../Microservices/Backend-For-Frontend.md), or directly). It may also respond to business events emitted from an [Event Backbone](../EventDrivenSystems/Event-Backbone.md) if those events are relevant to the user. This interaction is shown below. 

![Interaction Model Architecture](InteractionModel.png)

Interaction Models are related to specific business processes.  The same boundaries that apply to Domain Models (for instance, those found in the Event Storming process) also apply to the Interaction Model, since the Interaction Model captures the interactions with the users that lead to the actions and events in the Event model.  Likewise, Interaction Models are also often specific to a particular User Persona as a single business process usually has transition points where the focus shifts between different personas; each individual section between the intersection of business process and persona would be its own Interaction Model.

Interaction Models can be composed (See [Micro Frontend](Micro-Frontend.md) and [Chatbot](Chatbot.md) for examples of this).  In fact, you can even have interaction models of one type embedded into interaction models of another type (e.g. Hybrid Mobile Applications are a way of embedding Single Page Applications inside a Native Mobile Application).

One important consideration is that you should have common code (or at least dependency injection aspects) to deal with tracing and observability that make it possible to trace requests through all layers of the system regardless of the particular UI being used.  It’s also important to have a common user representation that goes across all of the different interaction models in the system.  

Finally, relating back to the discussion at the beginning of the chapter, Interaction Models can be classified as “Adapters” in a *Hexagonal Architecture* from [Cockburn](https://alistair.cockburn.us/hexagonal-architecture/). However, there are other types of adapters in this model that are not Interaction Models – you don’t want to take the analogy too far.  An Interaction Model may be distinguished by the fact that there is a human ultimately on one end of the interaction and not a system or other piece of software.  This is not a hard and fast rule, as there will always be ways to simulate human interaction or automate a system that is designed to interact with a human (such as user interface testing software like Selenium).  However at least part of the software design process should be devoted to making sure that the interaction can be carried out with a human in mind. Thus, it is intimately and inextricably tied into issues of user experience and UI design.  An upfront Design Thinking approach should always be employed in the development of an Interaction Model to ensure these issues are considered.

* * *

The Interaction Model is a broadened view of the *Application Controller* pattern from [POEAA].  That pattern was also concerned with the separation of UI from business logic, and sequencing or selecting UI operations, but is more tightly tied to page-based web interface technology, which is only one subset of the Interaction Model – see [Web Application](Web-Application.md) and its newer descendants, [Single Page Application](Single-Page-Application.md) and Micro Frontend.  However, the idea of business logic separation and explicit modeling of user interaction expands to many other areas as well – such as Native Mobile Applications, Chatbots, and Social Media Plugins.
