---
title: Cloud Refactoring
parent: Cloud Adoption
---
# Cloud Refactoring

You want to migrate an existing application onto the cloud.  You have a little bit of leeway on how many changes you can make to the application and its configuration but you are under time and budget constraints.

**How do you minimally adapt an existing application to work on the Cloud?  You can't afford to rewrite the application from scratch, but you do need to adapt it to take advantage of the features of a PaaS.**

One of the misconceptions of Cloud computing is that you have to adopt all of the new technologies that make up a Platform as a Service all at once.  However, it doesn't have to all happen at once.  You can incrementally update your application code, your deployment and management processes and your user experience.

Therefore,

**Perform Cloud Refactoring to change the most egregious dependencies on existing environments until the application can easily be deployed as PaaS components.  Over time you may refactor more components one at a time to adopt more cloud-native technologies.**

Some steps that can guide you along that journey are:

*Fix the biggest issues things only.*  There are certain aspects of running on a PaaS that are, in some ways non-negotiable.  PaaS's are generally not going have the same networking configuration as your on-premise systems, so reconfiguring your application to, for instance, look up IP addresses and host names from a configuration system or file will be a step in the right direction.  The individual runtime instances in a PaaS (such as a Cloud Foundry runtime or a Docker image) are generally not going to have the same level of uptime as a carefully managed local machine or on-premise VM. So another step would be to make sure that you can support a high enough level of redundancy in your application that the overall application functionality can survive the loss of a single runtime instance.

As part of this effort, you want to also *think about revisiting your application packaging structure and adapting some new packaging practices* without even changing your code.  A common issue in many application teams using Java is that over time they have built ever-larger EAR files to contain our logical applications so that those applications could be more easily deployed to all the application servers in a corporate farm.  The problem is this tied each piece of code in that application to the same deployment schedules, and the same physical servers.  If you changed anything you’d have to retest everything, and that made any changes too expensive to consider.  But now with PaaS technologies the economics have changed.  So one simple place to start is in reconsidering your packaging.  There are three principles that you can apply:

1. Split up your EARs: Instead of packaging all of your related WARs in one EAR you split them up into their independent WARs.  Note that this may involve some minor changes to code or more likely to static content if you change application context roots to be separate.
2. Apply [Container Per Service](../Cloud-Native-DevOps/Container-Per-Service.md): Next apply the *Container per Service* pattern and deploy each WAR in its own Liberty or Tomcat server – preferably in its own container (e.g. a Docker container or a Cloud Foundry instant runtime).  You can then scale containers independently.
3. Build, deploy and Manage independently: Once the WAR's are split, you can then manage each WAR independently through a separate automated [Devops pipeline](../Cloud-Native-DevOps/CD-Pipeline.md).  This is a step toward gaining the advantages of continuous delivery. 

*Look for ways to evolve your operations processes and toolsuite incrementally.*  One of the most common complaints about moving to a PaaS is that operations teams claim that they will not have the same level of insight or control over production applications as they currently do over on-premises versions of those applications.  But instead of making this a blocker for a move to a PaaS, look for ways to compromise without sacrificing the most important aspects of the partnership between development and operations.  One way to do this is to keep two separate, but very similar development pipelines.  Instead of starting off with a single development pipeline that can push an application all the way to production, have one pipeline that can be kicked off by development that can deploy into every stage aside from production.  Build a second development pipeline derived from the first, but that may perform additional checks and tests such as security scans and corporate compliance scans and that is capable of pushing the application into production, and then lock down that pipeline to only members of the operations team.

*Apply the [Strangler Application](Strangler-App.md) Pattern.*  The Strangler Application is an approach that works very well in Cloud Refactoring as an aid to incrementally updating the technologies used in an application, especially new user interface technologies.
