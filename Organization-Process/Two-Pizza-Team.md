---
parent: Organization and Process Patterns
title: Two Pizza Team
---
# Two Pizza Team

You are implementing a Cloud Native Design or implementing Cloud Refactoring.  You need to decide how big your teams can get in order to keep team productivity at its highest peak.

**How large should a team get before it becomes too unwieldly?**

There is a tension that everyone who has been in any software development team of any size has ever experienced - how big is too big and how small is too small?  There are small software projects that can be accomplished by a dedicated team of one or two people, but most software projects will require a larger team.  However, as Fred Brooks first pointed out in [The Mythical Man Month](https://www.amazon.com/Mythical-Man-Month-Software-Engineering-Anniversary/dp/0201835959) as the size of a software development team increases, the rate at which the code can be produced actually slows down as the number of potential communications paths between people (which is reflected in the software, aka [Conway's Law](https://www.melconway.com/Home/Conways_Law.html)) increases.  

What's more, there is an abundance of social science research that shows that humans simply perform better in smaller groups, and that our ability to form trusted relationships tends to max out in the low double digits, for instance, see [Dunbar](https://www.ncbi.nlm.nih.gov/pmc/articles/PMC3712454/) or also [Mueller](https://www.sciencedirect.com/science/article/abs/pii/S0749597811001105).  However, software is a complex entity.  There are a lot of steps required to plan, write and test a large program.  One of the things that Agile development has shown is that handoffs create friction.  Reducing handoffs between formal teams is critical to achieving rapid releases.  So, including all of the necessary skills within a team is crucial - you can't "outsource" a critical step in the software development process and still remain Agile.

What we have seen in practice, is that there are two alternative approaches to building teams on the cloud that we have seen that both result in failure; first trying to let developers "go it alone" on the cloud without support, and next, trying to start massive, enterprise-wide projects for cloud adoption all at once.  In the first case, you are not providing developers with all of the tools and support (particularly with learning) that they need.  In the second case, you find that the large numbers of people in existing, often role-based teams results in organizational inertia - no one is willing to make the changes necessary to be successful with new approaches and tools. 

Therefore,

**Make teams small, self-sufficient entities that have all necessary expertise on board (development, operations, testing, business, etcetera) but keep them to a size where two pizzas are sufficient to provide lunch/dinner for the whole team.**

Anecdotally, this limitation to team size is attributed to Jeff Bezos.  

When you look at the result of forming a team of this size and composition, what you see is that the ability to form trusted relationships in the smaller group facilitates the adoption of new approaches and new tools and processes.  What's more, you see that the team can be large enough to support some specialization, which is required in software development, but not so large as to enforce it - encouraging cross-training and the spread of skills around the group.

Keeping teams at this size will also encourage [Frequent Releases](), as the team will not grow so large that conflicts become too common and resolution of code conflicts becomes a major issue.  However, this will only work with a strict division of labor that keeps teams out of each other's way as the division of your organization both into domain-focused [Stream Teams](Stream-Team.md) and [Platform Teams](Platform-Team.md) will require.
