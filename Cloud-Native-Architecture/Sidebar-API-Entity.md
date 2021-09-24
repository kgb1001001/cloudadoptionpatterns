---
title: Api or Objects - which first?
parent: Microservices Design
---
# Which comes first: the API or the objects?

An ongoing argument exists about which comes first: the design of your API or the design of the Objects that implement your API. Many early distributed-computing proponents advocated designing the Objects first and then making your API the same as your Object API. This approach led to problems in the granularity of the API, which often resulted in APIs that represented technical interfaces instead of business interfaces.

When you start with the API, you can focus on solving the business problem and avoid getting lost in the technical details of a particular implementation. Pact testing is a slightly different version of API-first. Pact is a contract unit-testing tool that ensures that services can communicate with each other.

When you write PACT tests, you unit-test the consumer and the provider separately. To test the consumer of an API, you submit an actual API request to a mock provider and receive a response. To test the provider, a mock consumer issues a request and the provider provides an actual response. Verification is done in the mocked code to ensure that the services work as expected. Testing is done only on the specific functions that the customer uses.

The next consideration when you design an API is whether your APIs represent Entities or Functions. The starting point for mapping is the Resource API pattern (Daigneau 2011). This pattern is a stripped-down definition of the central idea of REST. You assign all procedures and instances of domain data a URI and then use the application protocol of HTTP to define the standard service behaviors by using standard status codes wherever possible. In this model, a request consists of a URI, an HTTP server method, and optionally, and rarely, a Media type. That combination uniquely selects the particular Service that fulfills the request.

The key notion is that each URI represents a Resource, not a procedure. Resource APIs must be the bulk of the APIs that you specify. They're the rule rather than the exception.

However, exceptions exist. The best way to handle non-entity Services is to think through the problem of "noun-ifying" them with the Process API pattern. A Process API is a reification of an action in a domain. If you can name a Service as a noun in Domain-Driven Design, that Service name becomes the URI path. A good rule is that if a paper-and-pencil version of the thing exists, it can become a resource, but if it’s something a person must do, it becomes a process. An example of a process API might be processing a purchase order.

When you start with Domain-Driven Design, you find that the large-grained concepts that are derived through the process are closer to the right level for a good API design:

* Aggregates and Entities become Resource APIs
* Value Objects inform the design of the schema that the Resource API uses
* Services become Process APIs
