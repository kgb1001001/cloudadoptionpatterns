---
title: What's the right size for a Microservice?
parent: Microservices Design
---
# What’s the right size for a Microservice?

It seems that the Microservices architecture has finally started to become well entrenched as an architectural pattern.  The [seminal paper on the subject](https://martinfowler.com/articles/microservices.html) by Martin Fowler and James Lewis turned six years old this past month, and it seems we can’t have an architectural discussion with anyone without the subject coming up at least once, if not being the entire subject of the conversation. 

As with any new technology, Microservices have followed the inevitable [Gartner hype curve](https://www.gartner.com/en/research/methodologies/gartner-hype-cycle).  From what we are gathering in the twitter-verse, it’s somewhere between the depths of the trough of disillusionment or starting the climb up the early part of the slope of enlightenment. That means that over the last six or so years, we’ve learned some important lessons about building Microservices, and one of those lessons has to do with making sure that you think about the scope of each Microservice in the proper way.

You see, the very name Microservices tends to lead people in a direction that may take them off into the deep weeds beside the side of the road they actually want to travel.  When you think of the term “Microservices”, the first thing that catches your eye is the prefix “Micro”.  Now, according to my handy-dandy college Classical Greek textbook , μικρός would only have meant little or small to Plato or Aristotle.  However, in everyday English usage, “Micro” tends to denote something astonishingly small - after all, a “Micrometer” is a millionth of a meter, and you use a “Microscope” to see things that are otherwise invisible to the naked eye because of their extremely small size.

It’s in that difference of perception that the trouble lies.  A Microservice should be “small” in comparison to the enormous monoliths that came before it.  However, it shouldn’t be too small - trying to make your Microservices too small is probably one of the most common mistakes teams fall into when attempting to implement a Microservices architecture.

It’s this thought that “Microservices must be tiny” that leads me to our first problem.  One of the other common complaints we hear about Microservices is that it’s too difficult to use them for complex domains like Banking because the REST or messaging interfaces they require don’t provide a way to do two-phase commits across multiple Microservices.  Whenever we hear that complaint, it sets off warning bells in our heads - that complaint is often a symptom that the team is thinking of their Microservices as very tiny things.  To resolve this, let’s start with a simple, toy example of that kind of thinking and look for a way to resolve it, then back up and think a bit more about the ramifications of that solution for a Microservices architecture as a whole.

We’ll begin with a simple design for an Account service, starting with a design that doesn’t yet include the Microservice implementation just so that we can see how it evolves.  Let’s say that the team is applying Domain Driven Design (more on that later) and in their first go-round they discover the need for an Account Entity that references a couple of associated dependent Entities – Entries and Owners. 
 
Pretty quickly the team discovers that there are some well-defined operations on the Account; debit, credit, open and close.  Luckily these operations map very well to a REST interface, so it’s relatively easy to take this simple Entity-based design and map it to a microservices implementation.  However, the problem comes in just a little bit later when they make a discovery – they haven’t worked out how to do transfers between accounts, as the following diagram shows:

 


The thing is that the whole idea of transferring between accounts is going to require a whole new REST interface – that much is obvious.  The question is how do you implement and does this represent an entirely new Microservice?

The simplest assumption (and one many teams fall into) is assuming that there should be a 1-1 map between Microservices and REST interfaces.  However, when we apply that equivalence to our example, we quickly run into a problem.  How would we implement that new Microservice?  The easiest way seems to be just to have the Transfer Microservice call the Account Microservice twice; once for a debit from the “from” account and once for a credit to the “to” account.  So our implementation might look something like this:

 
But this runs us right into the two-phase commit problem that we talked about earlier!  If the debit succeeds and the credit fails, then the poor customer is left with less money in their account than they used to have, but without any recourse.   This is obviously not acceptable in this situation; so many teams try the following solution instead:

 

This resolves the two-phase commit problem, but now what we’ve done is introduce coupling at the database. We’ve just violated one of the principles of Microservice design, which is that services should own their data and not have “hidden” coupling through a shared database.  So what’s the right answer?  Unfortunately, many teams then go (in my opinion) far off the deep end and start pursuing solutions involving the Saga pattern in order to handle the issue through compensating transactions.  However, while the Saga pattern does have its place, it’s not the right default solution for a simple situation like this.

Let’s consider the following solution instead, which challenges one of the earlier assumptions:

 

What we’ve done in this solution is to reconsider what we assumed to be a constraint – that one Microservice exactly equals one REST interface.  This assumption has been coded into dozens of Microservices tutorials on the web.  However, if you carefully read Fowler’s original paper, you’ll see that this assumption is never specified.   But that wasn’t really the point of this little exercise.  Instead, we want to zoom way back out and then use this exercise to illuminate a much broader set of problems.

Earlier on, we said that the team in our example had used Domain Driven Design (DDD) as part of their Microservices design process .  In that respect, the team was right on target.  One of the biggest problems that we see in the field with teams building Microservices designs is that they don’t often start with a technique like Domain Driven Design.  Instead, they start somewhere else, like with the design of their existing system, and try to derive their Microservices from there.  Or, else they start with an architecture (often specified in terms of tools and frameworks) and try to just let the Microservices evolve “organically”. In both cases, what you end up with are not what I would call Microservices – they tend to be very technology-focused and not at all related to terms that the business would recognize.  Instead, we tend to refer to the ones that are framed in terms of the words that the business would recognize as “Business Microservices” – and try to locate those in a design.   A symptom of inadequate design is that there are few or no Business Microservices in the solution, because you didn’t start with the business vocabulary.  Starting with the business vocabulary is a critical first step, and that’s why we suggest that all teams building Microservices apply Domain Driven Design as part of their design process.

If you do not start with the business vocabulary first, you often end up with an architecture that may look like the following:

 
Now, many of you may look at this and say “What’s at all wrong with this?  This looks like our own Microservices Architecture!”  To answer that, we have to go all the way back to a point that Fowler made in his original Microservices paper.  One of the points he and Lewis made is that when you have teams organized by technical expertise, that the software you produce will also be organized by technical area – this is simply Conway’s Law in action.   His solution is that you should have cross-functional teams organized by business capabilities instead.

But when you develop a Microservices architecture that looks like the previous, you have essentially gone all the way back to the problem that Microservices were intended to solve!  You’ve not only recreated the monolith, but you’ve made it worse by creating a distributed monolith.  This violates what is possibly the most important sentence Martin ever wrote:

*Fowler’s First Law of Distributed Objects:  Don’t distribute your objects.*

So what should your architecture look like instead?  Well, at the top level, just imagine drawing the lines vertically instead of horizontally.

 

This is in a nutshell what a Microservices architecture should look like from 50,000 feet.  The architecture should consist of a set of independent services, organized by business domain, and not oriented in complex end-to-end networks dictated by separation of technology areas.  Now that we’ve reset to that, then we face the question we originally posed at the beginning of the article – how big should each microservice be?  Let’s start with a lower bound, and then work our way up to a proposed upper bound.

*Lower bound:  A Microservice should consist of no less than an Aggregate (or at least an independent Entity) and the associated Services that operate on the entities of that Aggregate.*

In order to understand that definition, we have to make sure you’re familiar with two of the terms we are referring to.  An Aggregate is a concept from Domain Driven Design, and one that we’ve already seen a concrete example of.   Aggregates are groups of related entities whose lifecycles are tied together, allowing them to be treated as a single unit.  The canonical example of that is the Order/LineItem relationship, of which our Account/Entry example is just a variant.  

The second term is also a familiar one but perhaps not in the way you’re thinking of it.  We are using the term in the way that DDD defines a Service.  A Service is a “reification” of a function  - the “Transfer” that we called out in our earlier example is the canonical example of that idea.  In his book, Evens suggests we model those objects as standalone interfaces called Services that are stateless and whose interface is defined in terms of other elements of your domain model (Entities and Value Objects).  The key is that here a Service refers to a domain concept that does not naturally correspond to any particular Entity or Value Object

The most important design point here is that when thinking about how small to make your microservices, you have to think very, very carefully about transaction boundaries.  First of all you have to think about the lifecycle of the Entities involved in your Microservice – the create/read/update/delete cycle that we always think about in terms of persistence.  But then you have to extend your thinking to all of the updates that can happen to groups of these entities – these are the kinds of things that Service Objects will identify.  However, it’s not just simple one-to-one transactions like transfers you need to think about – you need to think more widely in the domain about other operations on groups of entities – particularly around things like batch updates and complex queries.

At this point, some purists may be shouting, “But wait! This would require 10, maybe 20 separate REST interfaces on my Microservice!”  That may be true.  If the particular area of your domain is complex enough to warrant that many operations on a single set of entities, then that is the smallest unit that you should be releasing as your microservice.  It may feel more like a mini-monolith, but it’s still better than trying to solve the problems that trying to split it any smaller would create.

What we have found is that it is always better to initially err on side of making a microservice too large than too small. It is easier to take a larger (coarser grained) microservice and split it into two than it is to take two fine-grained microservices and combine them.

## Finding the right level of abstraction

If this is the right lower bound for a microservices design, then how do you practically go about identifying all of those aggregates and especially the services that go along with those aggregates?  Luckily, the Domain Driven Design community has recently (in the last couple of years) come up with a very good answer to that question – start your design process by performing Event Storming.

Event Storming (described at https://www.eventstorming.com/, and also at https://www.ibm.com/cloud/architecture/architecture/practices/event-storming-methodology-architecture) is a workshop and process invented by Alberto Brandolini that allows a team to use sticky notes and whiteboards to quickly identify the most important Events within a business domain, to orient those events into a time sequence, and then to identify the Commands that kick off the events, the Data that is required to execute those commands, and the Policies that represent the logic required for one event to follow from another. 

What we have discovered in the time that we have been using the Event Storming process with our customers is that it gives you a repeatable, easily understood method for identifying your Entities and Aggregates as they emerge from discussing the vocabulary of the domain with experts in the domain.  But the most important part is that it doesn’t just show you the structure of the Data in terms of Entities and Aggregates – it also very importantly shows the Commands by which users operate on those entities to create Events, and the far-to-often hidden “Policies” that connect the pieces of the system together with business logic.    We won’t walk you through the entire process (but you can see a fully worked out example of the process here: ) but I will show you a sample result of carrying out a workshop.

 

In Event Storming, the Yellow stickies are the Users (expressed as personas) that operate on a system.  The Green stickies are the Data elements (Aggregates, or the occasional lone Entity) that the Users interact with through Commands (Blue stickies).  The Orange stickies are the Events that are generated as a result of executing the commands, or through receiving some sort of communication from another external entity, or possibly through the execution of business logic in the form of a policy.

But what’s important is this final arrangement.  As you see, the Commands that operate on a particular set of data, generating a particular set of Events, are all grouped together.  This forms a really good first-pass design for a Microservice at the right level of granularity.  That’s because the process itself tends to separate the different actors and the events that they interact with the system throughout very early.  What you end up with is a design that is very outside-in and that avoids much of the premature optimization that results when we focus just on the data structures or the purely technical aspects of the interaction between the microservices.  However, you should remember that this is only a first pass. It is very difficult to get the granularity of a microservice right on the first attempt. You need to plan to iterate on the design a few times to get the granularity right.

So if an aggregate and its associated service object are the right lower bound for the size of a Microservice, then what is the right upper bound?  Here I’m going to shift completely away from the discussion we’ve been having about Domain Driven Design and move over to an entirely different problem:

*Upper Bound:  A Microservice shall be no larger than that which allows a two-pizza team to release a single complete, appropriately sized user story to production within a single day.* 

Now we’ve really gotten some of you up in arms.  Some of you are already yelling “But that depends on what kind of CI/CD tooling you have, and your testing process, and your QA process, and the size of your user story, and even the velocity of your team!”  To which our response is EXACTLY.

Look, the whole reason why the industry is adopting Microservices is so that teams can release software faster, and with fewer problems.  By now most of you have read Nicole Forsgren et. al.’s wonderful book “Accelerate: The Science of Lean Software and DevOps: Building and Scaling High Performing Technology Organizations”.  In that book, one of the most important statistics that the team calls out from their research is the fact that they have correlated software delivery performance tempo – how frequently a team can release – to a number of other factors that determine a high-performing team.  Essentially the teams that perform the best are also the teams that can release the most frequently. And that gets right to the heart of the problem illustrated above.

The entire reason Microservices are more attractive than monoliths is that they reduce the set of problems that we’ve had with monoliths – the fact that testing cycles for monoliths can stretch into days or weeks, and the fact that monoliths are so complex that it makes modification or extension of them challenging or impossible.  But if your team can add a new feature within a single day, then by definition you are not hindered by either your testing cycle or by the complexity of modification or change.

But that leads to a slightly different set of complaints – when we suggest this sort of tempo to teams they start coming up with reasons why they can never meet this kind of rapid release cycle.  They start talking about the overhead of their “Agile” processes like daily standups that last hours, or top-down dictates to use tools like Jira that slow them down, or even worse, the need to go through change boards before anything can be released into production.  If that is your problem then we have a different, and even more controversial suggestion:

*Don’t try to adopt Microservices at scale unless you already understand and have successfully implemented Agile approaches and DevOps Principles such as automated testing and continuous integration.  Make sure you can walk the walk before you talk the talk*

One more possible litmus test to apply on the upper bound is to look at what business capabilities will go down if your microservice were to fail.  It there are more than one business capabilities that you would lose then either your microservice is too coarse grained and you should refactor it, or you have a different problem in that you have too many business processes depending on this one particular microservice (e.g. you put it on the critical path of several different flows).  

And that is where we have to conclude this particular article.  Microservices are a wonderful architectural innovation that has the potential to reverse problems we have encountered with monolithic architectures that have arisen over many years.  When implemented at the right level of granularity, they have substantial benefits in making a system more nimble and in reducing the blast radius of decisions. 

But Microservices are not a panacea.  They require teams to already be substantially mature in DevOps and Agile practices before they can be successful in applying them.   Microservices design should always be an iterative process.  If your team is not able to adopt that iterative process, then either the technology is not the right one for your team, or your team needs to change. We have found that you typically do not really know if the granularity of a set of Microservices is correct until you have a request for change of the system.  If you find that the change to implement a new business capability requires changes to several Business Microservices then we likely did not have the correct granularity (your microservices were too fine grained).  On the other hand, if the amount of testing required to release the change/new feature is disproportionately too long compared to the coding effort, your design is likely too coarse grained.  In either case, the solution is to make the appropriate change, but then learn from the experience and change your process to avoid the issue with other microservices in the future. 

