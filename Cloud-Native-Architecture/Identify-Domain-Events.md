You are starting on a Cloud-Native design and have already begun the process of Domain Driven Design.  You have identified some candidate Entities, Aggregates, and Potential Services.

**How do you figure out how all of these disparate pieces of domain driven design tie together in a dynamic system?**

One of the complaints that many people have had about Domain-Driven Design is that it seems to be concerned only with the static functionality of the system.  The patterns in [Evans]() are good for understanding the vocabulary (the Ubiquitous Language) of a business domain, but many practitioners have struggled to determine how to translate the pieces of the Ubiquitous Language expressed as Entities, Aggregates and Services into a complete and functioning system.

What is missing is a view of how the data *changes* through its lifecycle.  You need a dynamic view that allows you to understand how data is created, how it flows through the system, and how the system should react in response to changes introduced from the outside world.   *Events* provide just that kind of viewpoint that is needed to augment the static viewpoint of Entities, Aggregates and Value Objects. 

*Therefore,*

**Apply [Event Storming](https://www.eventstorming.com/book/) as a process to elucidate the set of Events that flow through a system and are captured and managed by the Entities, Aggregates and Services of a system**

Once you hae applied *Event Storming* you will find that you are well on your way to beginning to implement an [Event-Driven-Architecture](Event-Driven-Architecture.md)
