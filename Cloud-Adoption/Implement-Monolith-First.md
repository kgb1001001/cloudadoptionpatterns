# Implement Monolith First

Sometimes, time is of an essence in a greenfield project and microservices are known to add overhead.

**How do I launch a new application quickly?**

Greenfield projects can be built either in completely new companies (like a startup company), or in projects run within an existing company but having a lot of the properties of a startup. It is quite possible that, for example for compliance reasons, the company's existing infrastructure is not available for deployment, leaving a project team with a completely blank slate.

Regardless of whether in a startup or as part of an existing company, such projects usually also face significant time pressure. An early software startup needs to prove, with code, that its ideas are sound. A team in an existing company often has a sponsor that may very well act in the same manner as a venture capitalist.

In either case, time is of an essence and developing or acquiring a microservices platform to do it right the first time usually does not provide any business value at this stage. Ideas need to be proven, and whether these ideas are quickly jotted down or carefully calligraphed is of no consequence.

Therefore:

**Implement a monolith first. Refactor to a microservices architecture only if the application is sufficiently complex to warrant refactoring, and after the application has proven it is worth its salt.**

Teams in this situation often grab for very fast development stacks. An extremely popular choice in the startup world is, for example, Ruby on Rails with deployment on a public PaaS provider like Heroku. There is almost zero friction in moving such an application from the development environment to the production environment, and pretty much from day one the team is able to continuously release and show progress to their sponsor. With the focus on business logic, the team's time is spent very effectively at this stage; more effectively than when the team would distract itself with doing things "the right way", because the right way is simply not known at this stage: when the application is not successul, the right decision is to shut it down, not to rearchitect it into something more beautiful.

It's also quite possible (and common) to containerize these "mini-monoliths".  This is not quite in conflict with the advice to implement [One Service Per Container](Container-Per-Service.md) in that given the size of the application, the container footprint would still be relatively small. Grabbing a technology stack image from DockerHub and then deploying to a public Container-As-A-Service is also a quick, easy, lightweight way to get started quickly.

What does need to be kept in mind, is that *if* the application is successful, it will probably see more investment in terms of adding development capacity and more load in terms of usage. There will be a point in time when the initial monolith will be deemed cumbersome because neither development effort nor usage scale well with monolithic applications.

It is therefore extremely helpful if the team aims for success and keeps in mind that later on, having [Hairline Cracks](Look-For-Hairline-Cracks.md) in the application will make breaking it up simpler. If not, a [Strangler Application](Strangler-App.md) strategy may need to be followed to replace the monolith with new services, which is usually more expensive.

Martin Fowler first [discovered this pattern](https://martinfowler.com/bliki/MonolithFirst.html).

