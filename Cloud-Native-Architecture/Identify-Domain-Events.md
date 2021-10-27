---
title: Event Storming
parent: Microservices Design
---
# Event Storming

You are starting on a Cloud-Native design and have already begun the process of Domain Driven Design.  You have identified some candidate Entities, Aggregates, and Potential Services.

**How do you figure out how all of these disparate pieces of domain driven design tie together in a dynamic system?**

One of the complaints that many people have had about Domain-Driven Design is that it seems to be concerned only with the static functionality of the system.  The patterns in [Evans]() are good for understanding the vocabulary (the Ubiquitous Language) of a business domain, but many practitioners have struggled to determine how to translate the pieces of the Ubiquitous Language expressed as Entities, Aggregates and Services into a complete and functioning system.

What is missing is a view of how the data *changes* through its lifecycle.  You need a dynamic view that allows you to understand how data is created, how it flows through the system, and how the system should react in response to changes introduced from the outside world.   *Events* provide just that kind of viewpoint that is needed to augment the static viewpoint of Entities, Aggregates and Value Objects. 

*Therefore,*

**Apply [Event Storming](https://www.eventstorming.com/book/) as a process to elucidate the set of Events that flow through a system and are captured and managed by the Entities, Aggregates and Services of a system**

Event Storming is a brainstorming or design thinking technique developed by Alberto Brandolini that begins with a team writing down all of the "facts" about their system that they can think of on sticky (post-it) notes.  A fact should be expressed in past tense such as "deposit has been credited".  The team then arranges all of the facts they discovered in linear (time-sequence) order horizontally on a wall.  These facts are now Events in that they show how one occurence will be followed in time by another and another and another.  Where simultaneous events occur, they can be placed in different horizontal swim lanes separated vertically.

After the team agrees on the sequence(s) of events in time, they can then "decorate" the events by adding data that each event either requires or generates, "commands" that create an event, actors that cause commands to be issued, and policies that automatically turn one event into another.  The result of this is that a dynamic system design begins to emerge from the sequence of time-based events.

Finally, the events can be grouped together by data elements and related commands within a scenario to represent a complete bounded context.  In this way, the Event Storming approach has thus helped you to validate your Entities and Aggregates (they should be the same as you identified in earlier stages of Domain Driven Design) and you will be able to map specific commands to Services Objects.  Each Bounded Context that you identify then may become a candidate microservice.

Once you have applied Event Storming to *Identify Domain Events* you will find that you are well on your way to beginning to implement an [Event-Driven-Architecture](../Event-Based-Architecture/Event-Driven-Architecture.md)
