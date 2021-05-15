---
parent: Cloud Native DevOps
title: Red/Black Deploy
---
Red/Black Deploy
aka Blue/Green Deploy
===

When doing continuous deployment in a Microservices Architecture, especially with a [CI-CD Pipeline](CD-Pipeline.md), new service versions need to be rolled out quickly and safely. Classical methods of upgrading code did often require downtime, but user expectations have moved beyond that - services are expected to be able to be available.

**How can we safely and quickly deploy new versions of services?**

With cloud native environments, it becomes feasible to run both versions of the service in parallel. Classically, this would be too expensive as having a spare set of servers just for upgrades does not make business sence. These restrictions don't hold on a cloud environment where instances can be brought up and torn down on a whim.

Therefore:

**Deploy the new version on a new set of instances, running the current and new version in parallel. When the health of the new version has been verified, a simple load balancer switch can change to the new version; when problems arises, the same switch can be made back to the old version that is still active. Some time after everything checks out, the old version is torn down.**

Even when applications don't need to be available 24/7, modern development strategies often encourage a system where new versions are deployed as changes are ready. Waiting until a potential downtime window, even if possible, breaks this pattern and requires teams to work overtime and/or night shifts. So even though at first glance this strategy would only be useful for systems that cannot see downtime, it applies to a broad set of use cases and supports teams that prefer to roll out more releases each with smaller sets of changes, which is a proven method to reduce the risk associated
with software upgrades (citation needed).

This pattern is known as either "red/black" or "green/blue", but both names refer to the same strategy. The "red" or "green" cluster is the active one, the "black" or "blue" cluster is the stand-by one that runs the version that is not active.

On the public cloud, instances are paid for by the minute. It therefore makes financial sense to adopt a strategy that may seem wasteful at first. In effect, the cost of short bursts of redundant instances serves as an insurance premium against downtime. With modern deployment methods, the time that two instances are running is limited to half an hour or an hour and the additional cost is negligible.

The strategy does not prescribe the issues associated with rolling back versions, which gets progressively harder when changes in the data that the service stores are made. It is important that when red/black is adopted, that data changes are made in a manner that allows rollbacks.

The first place we encountered this pattern was in [this Netflix blog](http://techblog.netflix.com/2013/08/deploying-netflix-api.html), in the section "Multi-region Deployment Automation".
