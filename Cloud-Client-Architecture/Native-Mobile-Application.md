---
title: Native Mobile Application
parent: Cloud Client Architecture
---
Native Mobile Application
===

You are building applications that need to support on a variety of platforms. At the same time, most of your customers are going to use a Mobile device as their primary means of accessing your application.

**How do you provide the most optimized user experience on a mobile device and take advantage of the features that make mobile computing unique?**

There are several aspects of building mobile applications that are fundamentally different from building web applications:

-	Mobile device capabilities change and evolve quickly – Mobile devices have many attached sensors that users become accustomed to using in a variety of ways (scanning QR codes, or taking pictures of checks for instance) and at the same time provide unique features like haptic feedback that are not part of the web computing experience.
-	The two major Mobile ecosystems change rapidly. Applications that are built to emulate a mobile device look and feel often seem outdated when the native user interface libraries of the Mobile OS changes.  
-	Mobile devices, while rapidly improving, often do not have the same processing capability that larger desktop or tablet devices do.

While Single Page Applications provide a user interface that can be adapted to different screen sizes and orientations using Responsive Design no browser-based application can take advantage of all the features and capabilities of a mobile device. What’s more, even though advances have been made in the speed and performance of JavaScript in many browsers, the performance of browser-based applications still noticeably falls behind those of native applications. Another drawback of browser-based applications is that the user must remember to bookmark the webpage of the application – it is not present on their device home screen in the same way that native applications are present.

Therefore,

**Write a *Native Mobile Application* for both of the two major platforms (iOS and Android).**

For the reasons listed above developers have found that constantly used, highly interactive applications should be implemented as native applications using the tools and capabilities provide by the native development tool suite. This allows the developer to take maximum advantage of the platform’s capabilities, and at the same time allows users to easily locate and download the application through the platform’s application store.  For most capabilities in a mobile application, this will be the past of least resistance, and will allow the easiest use of new device capabilities as they evolve.

However, a design choice that many teams building Native Mobile Applications often struggle with is how much of their entire application space to implement in the Native Mobile Application.  In a Multichannel Architecture, you often have more user functions in the web application than may be available in the Mobile application.  In particular, there is the question of how to allow access to seldom-used functions from within a Native Mobile Application. Sometimes, teams have used native functions such as Web views to access the existing web content from within the Mobile application, but that often leaves users confused as the interface of the web application is not consistent with the native mobile application.  Instead, what has emerged as a solution to this problem is the use of frameworks such as React Native and Ionic that allow teams to embed application code written as Single Page Applications inside of existing iOS or Android applications.  The advantage of this approach is that React Native is compatible with existing web applications written using React, while likewise Ionic works with web applications written in React, Angular and Vue.  

An example of this kind of overall architectural approach is shown below:

![Mobile Application Architecture](../assets/NativeMobileApp.png)

Just as with [Single Page Applications](Single-Page-Application.md), microservices are a good match to *Native mobile applications* since the business-oriented capabilities of a *Business Microservice* map cleanly to the complex screen flow and interaction capabilities of a Native mobile application.

However, *Native Mobile Applications* have their own drawbacks that necessitate additional architectural decisions – most notably the
limited screen real estate of an application and the potentially poor Internet connectivity over a mobile network may necessitate the use of other patterns such as a *Near Cache* or *Backend for Frontend*.

*Native Mobile Applications* often are paired with [Backend for Frontends](Backend-For-Frontend.md) that can filter and translate results to data format that are specific to the Mobile platform. Likewise, *Native mobile applications* may benefit from a [Near Cache](Near-Cache.md) when Internet connectivity is slow or unreliable.
