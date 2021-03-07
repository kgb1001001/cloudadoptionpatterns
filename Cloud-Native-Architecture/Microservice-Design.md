# Microservice Design

You are embarking on developing an application using a *Microservices Architecture*. You understand the benefits of using microservices for new applications and refactoring applications to microservices, but you are usure how to start.

**How do you design the microservices that your application needs? What are the elements of a good microservices design?** 

The answers lie in some of the basic premises of object-oriented programming. The book Domain-Driven Design: Tackling Complexity in the Heart of Software (Evans 2004) captures a meta-process for designing software that object-oriented software development teams have used for years. The book isn't about specific design notations or even specific classes of objects or patterns. Instead, it covers the general categories of objects that good object-oriented designers identify and work with. Those categories become critical elements of a good microservices design.

*Therefore,*

**Follow a Domain Driven Design  and Event Driven Design Approach for identifying Microservices**

* Understand the [Bounded Context](Context.md) for this subdomain
* Start with [Identifying Entities and Aggregates](Identify-Entities-And-Aggregates.md)
* Next [Identify Repositories](Identify-Repositories-And-Services.md) and [Services](Services.md)
* Finally [Identify Domain Events]

*Putting it all together*

When you follow the Domain-Driven Design process, you end up with these object types:

* A list of Entities, some of which are Aggregates, including identified root Aggregates and Entities
* A set of Repositories
* A list of Value Objects that are associated with one or more Entities
* A list of Services that correspond to functions that aren't part of any particular Entity
* A list of Domain Events that connect the Entities, Aggregates and Services together

In summary, when you design microservices for an application, use the principles of Domain-Driven Design to guide you along the way. Establish the Bounded Context for your team and list your Entities, Repositories, Value Objects, Services and Domain Events within the Bounded Context. Then, use what you learned to define and design your microservices.

These object types are what you need to create your first-pass RESTful service design for microservices. Not all of these objects become part of your microservices design—some might be hidden in your service implementation—but you can start to understand the objects that you're dealing with.

*Which comes first: the API or the objects?*

An ongoing argument exists about which comes first: the design of your API or the design of the Objects that implement your API. Many early distributed-computing proponents advocated designing the Objects first and then making your API the same as your Object API. This approach led to problems in the granularity of the API, which often resulted in APIs that represented technical interfaces instead of business interfaces.

When you start with the API, you can focus on solving the business problem and avoid getting lost in the technical details of a particular implementation. Pact testing is a slightly different version of API-first. Pact is a contract unit-testing tool that ensures that services can communicate with each other.

When you write pact tests, you unit-test the consumer and the provider separately. To test the consumer of an API, you submit an actual API request to a mock provider and receive a response. To test the provider, a mock consumer issues a request and the provider provides an actual response. Verification is done in the mocked code to ensure that the services work as expected. Testing is done only on the specific functions that the customer uses.

The next consideration when you design an API is whether your APIs represent Entities or Functions. The starting point for mapping is the Resource API pattern (Daigneau 2011). This pattern is a stripped-down definition of the central idea of REST. You assign all procedures and instances of domain data a URI and then use the application protocol of HTTP to define the standard service behaviors by using standard status codes wherever possible. In this model, a request consists of a URI, an HTTP server method, and optionally, and rarely, a Media type. That combination uniquely selects the particular Service that fulfills the request.

The key notion is that each URI represents a Resource, not a procedure. Resource APIs must be the bulk of the APIs that you specify. They're the rule rather than the exception.

However, exceptions exist. The best way to handle non-entity Services is to think through the problem of "noun-ifying" them with the Process API pattern. A Process API is a reification of an action in a domain. If you can name a Service as a noun in Domain-Driven Design, that Service name becomes the URI path. A good rule is that if a paper-and-pencil version of the thing exists, it can become a resource, but if it’s something a person must do, it becomes a process. An example of a process API might be processing a purchase order.

When you start with Domain-Driven Design, you find that the large-grained concepts that are derived through the process are closer to the right level for a good API design:

* Aggregates and Entities become Resource APIs
* Value Objects inform the design of the schema that the Resource API uses
* Services become Process APIs
