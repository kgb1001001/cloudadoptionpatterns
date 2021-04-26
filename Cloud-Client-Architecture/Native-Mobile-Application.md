---
title: Native Mobile Application
parent: Cloud Client Architecture
---
Native Mobile Application
===

You are building applications that need to support on a variety of platforms. At the same time, most of your customers are going to use a Mobile device as their primary means of accessing your application.

**How do you provide the most optimized user experience on a mobile device and take advantage of the features that make mobile computing unique?**

-   Mobile device capabilities change and evolve quickly

-   Applications that are built to emulate a mobile device look and feel often seem outdated when the native user interface libraries of the Mobile OS changes

-   Mobile devices, while rapidly improving, often do not have the same processing capability that larger desktop or tablet devices do.

Therefore,

**Write a *Native Mobile Application* for both of the two major platforms (iOS and Android).**

While *Single Page Applications* provide a good user interface that can be adapted to different screen sizes and orientations using Responsive Design no browser-based application can take advantage of all the features and capabilities of a mobile device. What’s more, even though advances have been made in the speed and performance of Javascript in many browsers, the performance of browser-based applications still noticeably falls behind those of native applications. Another drawback of browser-based applications is that the user must remember to bookmark the webpage of the application – it is not present on their device home screen in the same way that native applications are present.

For these (and other) reasons, developers have found that constantly used, highly interactive applications, should be implemented as native applications using the tools and capabilities provide by the native development tool suite. This allows the developer to take maximum advantage of the platform’s capabilities, and at the same time allows users to easily locate and download the application through the platforms application store.

Just as with [Single Page Applications](Single-Page-Application.md), microservices are a good match to *Native mobile applications* since the business-oriented capabilities of a *Business Microservice* map cleanly to the complex screen flow and interaction capabilities of a Native mobile application.

However, *Native Mobile Applications* have their own drawbacks that necessitate additional architectural decisions – most notably the
limited screen real estate of an application and the potentially poor Internet connectivity over a mobile network may necessitate the use of other patterns such as a *Near Cache* or *Backend for Frontend*.

*Native Mobile Applications* often are paired with [Backend for Frontends](Backend-For-Frontend.md) that can filter and translate results to data format that are specific to the Mobile platform. Likewise, *Native mobile applications* may benefit from a [Near Cache](Near-Cache.md) when Internet connectivity is slow or unreliable.
