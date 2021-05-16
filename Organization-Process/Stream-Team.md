---
parent: Organization and Process Patterns
title: Stream Team
---
# Stream Team

You are either building a new application with [Cloud Centric Design]() or applying [Cloud Refactoring]() in order to modernize an existing application to run on the cloud.  

**How do you organize an application team to be able to successfully build an application for the cloud using [Cloud Native DevOps]() principles that also takes into account the constraints that architectural principles like the [Microservices Architecture](../Microservices/Microservices-Architecture.md) place on a team?**

The Two Pizza Team sounds simple in theory - just make sure your teams don't get much larger than 10-12 people (or if they do, have a go-to pizza tekeout that provides very, VERY large pizzas).  However, there is a lot implied in applying the Two Pizza Team idea to application development.

For most of the lifetime of Information Technology as a discipline, people have been organized by roles.  At first glance, that makes sense; after all, if you are going to do a testing phase, then you obviously need Testers, so shouldn't all of the Testers sit together and be organized under the same management structure in order to most efficiently apply these scarce human resources to the projects that need them the most?  However, this conclusion is based on a number of assumptions that simply do not hold true anymore.  First of all, the very idea of a separate "Phase" for activities such as Testing (or Development, or Operations, etc.) is based upon the assumption that development proceeds in a linear fashion across multiple aspects - that all the architecture and design happens first, followed by coding and development, followed by testing, and then finally by production deployment and operations.    In the past, when release cycles were measured in months or even years, this could be said to bre true.  However, as [Forsgren]() has pointed out, one of the most reliabile indicators of how well a team functions is how often they release code to production.  Today, release cycles for most software should be measured in at most days, if not hours.

When the Testing "Phase" disappears, what then becomes clear is that separating people by role is also questionable.  Agile Practices such as Test Driven Development, and improvements and advances in Test Automation have made testing of nearly all types the domain of the developer - perhaps more accurately, developers have been asked to acquire the skills that were formerly reserved to Testers.  The key observation is that handoffs between different roles takes time - if you can remove formal handoffs (which often require changes in tools, notation or data format) between roles then the overall pace of development accelerates. 

So, if you want a team to move quickly, you need to reduce the time it takes to move between the different SDLC aspects.  The best way to do that is to put all of the team mebers together, and to have the team members each participate (wherever possible) in every aspect to eliminate handoffs altogether.  

However, scaling is stil a problem - even if your team members can perform each of the SDLC aspects, there is only so much work that a team sized according to the Two-Pizza rule can do.  There needs to be a different way of dividing work if not by role.

Therefore,

**Divide the overall work up into multiple, independent (or loosely coupled) work streams, divided along domain lines.  Define one or more self-sufficient Stream Teams (one per workstream) that each are responsible for a well-defined portion of the application, and that are sized as [Two Pizza Teams](Two-Pizza-Team.md). Stream teams are responsible for building, testing, and deploying their portion of the application from end to end.** 

The advantages of dividing teams along domain lines, or more loosely, by saga, where a saga is a group of closely related User Stories, are accentuated when teams follow a [Microservices Architecture](../Microservices/Microservices-Architecture.md).  Conway's Law states that the communications paths of your Software Architecture will reflect the communications paths of your organization.  If you want to build a loosely coupled, domain-based software architecture, then organize your teams into autonomous units, each oriented around a particular aspect of your problem domain.
