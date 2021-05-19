---
title: Organization and Process Patterns
nav_order : 12
has_children: true
---
# Organization and Process Patterns

This section covers a small set of Organizational and Process Patterns that are required in order to successfully implement the more technical patterns that are foudn elsewhere in this pattern language.  It is not our intention in this Pattern Language to document all of the different aspects of Agile Development that are required to be successful with Adoption of the Cloud; there are other books such as [Forsgren](https://www.amazon.com/Accelerate-Software-Performing-Technology-Organizations/dp/1942788339), [Skelton](https://www.amazon.com/Team-Topologies-Organizing-Business-Technology/dp/1942788819) and [Reznick](https://www.amazon.com/Cloud-Native-Transformation-Practical-Innovation/dp/1492048909) that document those aspects already.

Instead, we would consider the set of patterns that we outline here to be the minimal set of constraints that are required in order to have a good chance of succeeding in a Cloud Adoption.  We discovered these patterns when we realized that it was impossible to talk about the more technical patterns without them being placed within the context of this minimal set of Process and Organization Patterns.  That small subset includes:

* [Two Pizza Team](Two-Pizza-Team.md) is fundamental in that it describes an important aspect about Cloud Adoption that is often overlooked - that humans work best in small groups.  There are two extremes that we have seen that both result in failure; trying to let developers "go it alone" on the cloud without support, and trying to start massive, enterprise-wide projects for cloud adoption all at once.  Two Pizza team describes how any successful transformation has to be built from small teams.

* [Stream Team](Stream-Team.md) describes the basic team structure of a team building an application for the cloud.  Teams need to be autonomous, cross-disciplinary and importantly, small enough to focus on one (and only one) particular aspect of a domain that they understand very well.  These teams need to be tied together to produce larger applications, but the basic unit still needs to be small enough to share lunch.

* [Platform Team](Platform-Team.md) is also foundational in that it recognizes the fact that Stream teams cannot go it alone without ensuring that they work together within a common platform, be that in a public cloud, private cloud, or even a [Hybrid Cloud Model](../Cloud-Native-Architecture/Hybrid-Cloud-Model.md).  

* [Frequent Releases] is a basic process principle that underlies many of the Agile practices and is the reason behind many DevOps patterns.  One of the main reasons to keep teams to a size of a [Two Pizza Team](Two-Pizza-Team.md) and employ architectural principles like the [Microservices Architecture]() is to make Frequent Releases possible.
