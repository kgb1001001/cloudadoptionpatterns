---
parent: Cloud Native DevOps
title: Pipeline
---
Pipeline
===

You are either building a new application with a [Cloud Centric Design](../Cloud-Adoption/Cloud-Centric-Design.md) or reimplementing an application as part of [Cloud Refactoring](../Cloud-Adoption/Cloud-Refactoring.md).

**How do you ensure that your application can be built, tested and deployed in an automated and standardized way?**

Therefore,

**Define a Pipeline of standard build and deployment stages.**

A Pipeline allows code to flow through a consistent, automated sequence of stages where each stage tests the code from a different perspective. Each stage requires the necessary automation to not only run tests but also provision, deploy, setup, and configure the stage. Code should progress through the stages in an automated fashion with as little human intervention as possible.

The pipeline should employ a number of different strategies that make deploying the artifacts pushed through the pipeline simpler.  One key strategy is the idea of a [Red-Black Deploy](Red-Black-Deploy.md) that allows for easy rollback.  [Canary Testing](Canary-Testing.md) is another useful approach that allows you to validate that your deployment will succeed at scale.  Another strategy that is often helpful is the [Feature Toggle](Feature-Toggle.md) which aids with the issue that you may want to push features out to different stages faster than you can certify them in that environnment.
