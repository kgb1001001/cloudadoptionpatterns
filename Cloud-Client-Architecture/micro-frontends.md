# Micro Frontends

You are developing a new web application or you are refactoring a section of a web application to make it more modern.

**How do you avoid creating a monolithic [Single Page Application](Single-Page-Application.md) by placing too much functionality in the front-end or forcing your architecture to a single application framework?**

* You want to allow teams to use multiple frameworks \(such as Angular or React\) without forcing a single framework.

* You want to allow teams to be able to independently develop and release functionality without deploying the entire UI

* You want to allow cross functional teams that own a feature from front-end to back-end.

**Split your Single Page Application into several Micro Frontends that align to features.**

A Micro Frontend, like a Single Page Application consists of HTML, CSS and Javascript.  Like Microservices and Single Page Applications, a Micro Frontend should be an independent, self-contained application that has no dependencies on other Micro Frontends or shared libraries.  For example a change to a Javascript library or CSS in one Micro Frontend should have no impact on any other Micro Frontend.

This level of isolation allows several Micro-Frontends to be placed on a single web page that can operate independent of each other, be deployed independently and even use different frameworks, for example 2 Micro Frontends on the same page could use Angular and React respectively.

To allow the team to own features and functionality from Frontend to Backend then the Micro Frontends should be aligned to the backend Microservices especially those Microservices that implement the [Backends for Frontends](../Microservices/Backend-For-Frontend.md) pattern

By implementing the Micro Frontend pattern you can develop and deploy small features with more agility than a Standard [Single Page Application](Single-Page-Application.md)  This enables cross functional teams, ownership of frameworks, end to end ownership of features and reduces complexity,

