---
parent: Cloud Native DevOps
title: Feature Toggle
---
Feature Toggle
===

You are building a cloud-native application using a [Microservices Architecture](../Microservices/Microservices-Architecture.md) and need to roll out the deployment of new functionality.

**How can we control the roll-out of potentially risky new functions?**

You want to enable early testing of your software without requiring every aspect of the software to be complete before testing begins.

You want to avoid having to have "feature branches" in your source code repositories, allowing for main-branch development.

**Build a software switch in the microservice that can enable or disable the functionality without having to redeploy. Have a mechanism to ramp-up the new functionality as needed (percentage of traffic, per user, per account, geographically, etcetera).**

Feature toggles are (in the simplest form) implemented as conditional code that simply looks for the presence or absence of a flag (perhaps a configuration, a global variable, or a value passed in as an HTTP header) before either enabling or disabling a new feature.

This [article](https://martinfowler.com/articles/feature-toggles.html) gives more information on implementation patterns of Feature Toggles.  Products such as [Launch Darkly](https://launchdarkly.com) implement Feature Toggles along with other incremental deployment features. 
