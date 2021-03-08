# Identify Entities and Aggregates

You are building an application following a Microservices Architecture.  You need to understand how to discover your microservices from a complex business domain.

**What concepts in a business domain best correspond to microservices?**

Designing for a monolith is a relatively easy process.  When you are not overly concerned about how difficult testing a system is, you can create objects or data structures corresponding to business concepts within the monolith as much as you please.  The problem comes in when you need to start understanding how different viewpoints of the same concept apply.  You often end up with either multiple classes with slightly different names and responsibilities, or (even worse) huge classes with very different responsibilities and vast amounts of shared data.

But when you begin with the problem of reducing testing and limiting the blast radius of decisions as part of a microservices approach, you find you have to take a more measured approach to dividing up the concepts in a domain.  You have to think carefully about the ownership and lifetime of each piece of data, and under what context different viewpoints apply.

Therefore,

**Start your microservices design by identifying the Entities and Aggregates in your domain.** 

An Entity is an object that is distinguished by its identity. Entities have unique identifiers. Entities also have attributes that might change, but the identifier for the person stays the same. An example of an entity is a person. A person has an unchanging identifier, such as a Social Security Number in the United States. That same person has a given name, a surname, an address, and a phone number. Any of the attributes can change, but the person doesn't change.

Evans notes that entity objects must have a well-defined lifecycle and a good definition of what the identity relationship is—what it means to be the same thing as another thing.

From Entity-Relationship modeling, you know that sometimes Entities might be well-defined and have a specific well-known identifier, but might not live independently. Evans calls the combination of Entities an Aggregate.

You can find a simple example of the Entity/Aggregate relationship in a retail store. If you go to the soda aisle in a grocery store, you can buy a 12-pack carton of soda. Each can in the carton has a bar code to identify it individually, but you can't buy a single can from the carton. The cans are entities that are referred to as Dependent Entities. The root entity is the carton. The carton is the Aggregate because it defines the Dependent Entities' lifecycle (at least as far as the retail store is concerned)

The opposite of an Entity is a Value Object. Value Objects have no conceptual identity. You can't tell one Value Object from any other of its type. If you treat all objects in a system as Entities, the process to assess and manage the identity of each object can become overwhelming and hurt performance. Instead, care only about the attributes of a Value Object and that each Value Object can be treated as unchanged from the creation of the object until it is destroyed.

Consider an example of a Value Object. When you go to the bank, you usually want to access your bank account. Your bank account is an entity. If you query your current account balance, the result is a Value Object. The next time that you query your account balance, a different Value Object is returned with your new current balance.

Usually, when you identify the Entities and Aggregates, most of the Value Objects "fall out" of the process.  You don't have to go explicitly looking for them, they simply start to accumulate - you just keep a running list of them as the process carries on.

Another thing to keep in mind is that Aggregates usually either succeed or fail as a whole. They often form the boundaries of transactionality. 

But be aware that Entities and Aggregates do not always equal Microservices on a one-to-one basis.  You also have to consider the dynamic flow of information through the system.

