---
title: Multimodal Architecture
parent: Cloud Client Architecture
---
# Multimodal Architecture (aka Multichannel Architecture)

You are building a new application or refactoring an existing application that needs to provide a rich user interface that can be usable on many different devices such as smartphones, tablets, or laptops.  However, you need to provide the absolutely best user experience on each device, and need the interface to be best-in-class on each platform.

This is complicated by the fact that you also need to support diverse user communities served by your application, which may mean that different user segments may prefer or default to one particular device type.  For example, in a financial services application, younger users may default to using a mobile application, while slightly older users may prefer the larger screens of a desktop application.  At the same time, the investment needs and preferences of younger and older users may also differ slightly, leading to small differences in capability or navigation between the application on different devices.

**How can an application’s user interface work on different device types, incorporating the strengths of each type, while providing consistent functionality across the types?**

When applications for mobile devices and even web applications were new, they were often implemented to duplicate the functionality of existing applications with less standardized user interfaces. This lead at best to duplicate logic requiring separate maintenance, and at worst to applications that provided inconsistent functionality depending on the user interface. (E.g., if the mobile app won’t allow something, maybe the web app will!) Business functionality must be separated and encapsulated, allowing multiple user interfaces to reuse it for consistency.
Your application design process is complicated by the following issues:

-	Modern devices have many more user-interaction capabilities than previous generations of devices that only supported mice and keyboards.  Mobile devices in particular support many more interaction styles than desktop applications do (for example, gestures) and also support input devices not supported by laptops (e.g. cameras and near-field communication).
-	Users expect more from their applications and websites today than they did when the web was first introduced.  Most users are sophisticated enough to know the capabilities of each platform from using other applications on the platform.  When an application runs on a particular platform, they expect it to leverage the capabilities of the platform, like wide screens on laptops, and GPS location on mobile devices.

However, there are also new capabilities that modern platforms give you that were not possible in earlier generations of web applications.  Web-based protocols such as REST make communication between applications running on any device and back-end services both straightforward and standardized.  Likewise, the growth of computing capability on devices (such as mobile devices and tablets) makes it possible to move as much interaction logic as needed directly into the device without unduly impacting performance.

But the point remains that it is difficult to build a single application in one form factor that serves all of a diverse user community at all points in the interaction lifecycle.  Perhaps the best example of this that we have encountered took place at a major airline.  In this airline, there are three major vehicles for customer interaction; the airline’s mobile application, the airline’s website, and the check-in kiosks available at the airport.  What we saw is that the same users would sometimes use all three points of interaction; they would buy tickets on the website, check in on the mobile application, but print bag tags from the kiosk!  Of course, there was significant functional overlap between all three points of interaction; you could, for example, print a boarding pass at home, or at the airport, or display a mobile boarding pass in the mobile application.

What is needed is a way to allow for all these different forms of interaction (and ones we have not even yet considered, such as SMS texting, social media sites, command line interfaces (CLIs), etc.) within a consistent and coherent architecture.  The application needs to enable the user to interact with the system the way they want, where they want. 

Therefore,

**Structure an application’s user interaction layer as a Multimodal Architecture that separates interaction logic from business logic and enables a custom user interface for each device type.**

An example of this type of architecture (drawn from the airline example) is shown in below.

![Airline Example](../assets/AirlineExample.png)

In this particular example, we were replacing three existing monolithic systems (one for each channel, e.g. web, kiosk, and mobile) by refactoring the code into two new *Single Page Applications* that both shared common code and that used a common *Backend for Frontend*.  We likewise refactored the existing mobile application to share the new common [Domain Microservices](../Microservices/Business-Microservice.md) and [Adapter Microservices](../Microservices/Adapter-Microservice.md) through a new *Backend for Frontend*.

This refactoring enabled us to keep the different user interaction types but take advantage of the commonality between them at the microservices layer, and thus reduce the overall code size.  It also enabled us to replace the existing systems over time as we applied the Strangler Application pattern as sections of the existing systems moved over to the new approach one at a time. The *Multimodal Architecture* pattern is independent of whether you are using a monolith or microservices approach, but in this case, it facilitated our transition to the microservices approach.

The *Multimodal Architecture* we adopted thus allowed us to keep the UI logic separate from the Domain logic, but also allowed us to support the user through multiple different user interface channels, all sharing a common domain back-end.  So, we could support ticket printing and bag tag printing on those platforms that had printers attached, but likewise take advantage of unique features like location services to provide features like interactive maps on mobile devices that were not available on either the Web site or Kiosk.

* * *

The *Multimodal Architecture* allows you to leverage different technologies to reach different user communities.  As we have seen, you can still build traditional [Web Applications](Web-Application.md) or intelligent front-ends such as [Native Mobile Applications](Native-Mobile-Application.md) or [Single Page Applications](Single-Page-Application.md) that interface with more general-purpose back-end services representing the resources within a business domain, e.g. [Domain Microservices](../Microservices/Business-Microservice.md). However, you can also use technologies like [Chatbots](Chatbot.md) for specialized user interaction types like customer support. [Document Generators](Document-Generator.md) are useful when you are producing special forms (such as airline tickets!) that must meet legal or regulatory requirements.  You usually will want to use [Backends for Frontends](../Microservices/Backend-For-Frontend.md) where needed to adapt between the needs of specific *Native Mobile Applications*, *Single Page Applications* and *Domain Microservices*. 
