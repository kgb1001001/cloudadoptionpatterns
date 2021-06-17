---
title: Multichannel Architecture
parent: Cloud Client Architecture
---
# Multichannel Architecture

You are building a new application or refactoring an existing application that needs to provide a rich user interface that can be usable on many different devices such as smartphones, tablets, or laptops.  However, you need to provide the absolutely best user experience on each device, and need to be best-in-class on each platform. 
This is complicated by the fact that you also need to support diverse user communities served by your application, which may mean that different user segments may prefer or default to one particular device type.  For instance, in a financial services application, younger users may default to using a mobile application, while slightly older users may prefer the larger screens of a desktop application.  At the same time, the investment needs and preferences of younger and older users may also differ slightly, leading to small differences in capability or navigation between the application on different devices.

**How do you design an application that meets the needs of your users while still working within the capabilities and leveraging the strengths of each of the different interface devices that now exist?**

Your application design process is complicated by the following issues:
-	Modern devices have many more user-interaction capabilities than previous generations of devices that only supported mice and keyboards.  Mobile devices in particular support many more interaction styles than desktop applications do (for instance gestures) and support input devices not supported by laptops (e.g. cameras and near-field communication). 
-	Users expect more from their applications and websites today than they did when the web was first introduced.  Most users are sophisticated enough to know the capabilities of each platform from using other applications on the platform.  When an application runs on a particular platform, they expect it to leverage the capabilities of the platform, like wide screens on laptops, and cameras on mobile devices.

However, there are also new capabilities that modern platforms give you that were not possible in earlier generations of web applications.  Web-based protocols such as REST make communication between applications running on any device and back-end services both straightforward and standardized.  Likewise, the growth of computing capability on devices (such as mobile devices and tablets) makes it possible to move as much interaction logic as needed directly into the device without unduly impacting performance.

Therefore,

**Adopt a *Multichannel Architecture* that combines intelligent, composable front-end User Experience components with general-purpose back-end business components.*

An example of this type of architecture is shown below.

![Modern Web Architecture](../assets/ModernWebArchitecture.png)

You can build intelligent front-ends either as [Native Mobile Applications](Native-Mobile-Application.md) or [Single Page Applications](Single-Page-Application.md) that interface with more general-purpose back-end services representing the resources within a business domain, e.g. [Domain Microservices](../Microservices/Business-Microservice.md). You can also use technologies like [Chatbots](Chatbot.md) for specialized user interaction types like customer support. You very often will want to use [Backends for Frontends](../Microservices/Backend-For-Frontend.md) where needed to adapt between the needs of specific Native Mobile Applications, SPA’s and Domain microservices. [Near Caches](Near-Cache.md) can improve the performance of your intelligent front-ends.
