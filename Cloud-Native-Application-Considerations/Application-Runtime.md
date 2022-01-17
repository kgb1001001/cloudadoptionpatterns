---
parent: Cloud Native Application Considerations
title: Application Runtime
---
# Application Runtime

You are implementing an application as a [Cloud-Native Application](Cloud-Native-Application.md).

**What computer language should you use to implement the application?**

There are lots of languages. Which ones work well for cloud? Why do some work well and others don't?

**Implement the application in a language with a separate runtime that can run in Linux.**

Runtime environments for Java include the Java Runtime Environment (JRE), Spring Boot, Open Liberty, and Quarkus. JavaScript runtime environments include Node.js (with NPM) and TypeScript. Go has the Go runtime and Python has the Python runtime. PHP, Ruby, and even COBOL have runtime environments. On the other hand, C, C++, and assembler don't have runtimes.

The way you will deploy an application to run on a cloud platform is that you (or the cloud platform) will install the application's programming languages' runtime onto the cloud platform's operating system (usually Linux) and then will deploy the application into the runtime. Once deployed, the application can be started and stopped when needed.

Each application has a different runtime and therefore can be implemented in a different computer language.
