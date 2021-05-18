---
parent: Organization and Process Patterns
title: Platform Team
---
# Platform Team

You are building one or more applications for the Cloud and you are following a [Hybrid Cloud Model](../Cloud-Native-Architecture/Hybrid-Cloud-Model.md) which results in you having several different environments; some on public cloud, and possibly some on private cloud.  You need to enable your [Stream Teams]() to be productive, without weighing them down with unnecessary infrastructure management.

**How do you create an organizational structure that enables Stream Teams to focus on creating business value through building applications and not become mired in the minutiae of cloud platform management?**

There is always an ongoing tension in companies adopting the cloud between how much autonomy to give teams developing applications, and how much control to centralize into the IT departnement.  Due to the fact that many Public Cloud projects are started by the Line of Business rather than by Centralized IT, this tension is exacerabated as IT has sturggled to find its place in the new world.  As a result, centralized IT often tries to reassert control by developing centralized private cloud services, either as a landing zone in a public cloud, or as an on-prem private cloud, but when these cloud environements are created without the direct involvement of the line of business teams, they often fall in to the trap of "if you build it they will come", where no one ever comes to the newly created environments.

Therefore,

**Create a common Platform Team that is responsible for developing and managing the components of a shared platform up through but not beyond the Container Orchestration layer**

The Platform Team is, importantly, a Team and not an environment.  They may be responsible for multiple environments, and may set standards for those environments, and build reusable assets that can be used by many teams, but they do not "put all of their eggs in one basket". The kinds of reusable assets produced by the Platform Team could include Base Images that are used by the Container DevOps, but also template CI/CD pipelines that the [Stream Teams](Stream-Team.md) can consume and customize. 

This pattern is discussed in depth in [Team Topologies](https://www.amazon.com/Team-Topologies-Organizing-Business-Technology/dp/1942788819).  One thing to keep in mind is that a Platform Team should not grow too large - it should ideally be no larger than a [Two Pizza Team](Two-Pizza-Team.md).  
