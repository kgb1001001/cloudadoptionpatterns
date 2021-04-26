---
title: Bounded Context
parent: Cloud Native Architecture
---
# Bounded Context

Your team is building applications using a Microservices Architecture.  Your Two Pizza Team is part of a much larger team, but you need to keep out of each others way as you develop your systems.

**How do you clearly define the "edges" of where the work your team performs abuts the work of other teams?**

The problem with a single domain model (e.g. a single vocabulary and set of code) that covers an entire domain is that it will often be too big to be manageable.  Human beings have limits to how much information they can easily keep in their heads at one time.  For instance, George  Miller's "The Magical Number Seven Plus or Minus Two" describes the limitations of our short-term memory. What's more, when more than one team shares a single common model, and common code base, the members of the teams will inevitably run into each other when making changes that are internally consistent to one team's view of the model, but inconsistent with another team's view.  This leads to one of the problems with Monolithic Applications - it becomes difficult to test components that simultaneously represent different viewpoints.

Therefore,

**Let each team have its own separate viewpoint on the conceptual model and it's own unique codebase representing that viewpoint.  Define a Bounded Context for each team.**

A Bounded Context explicitly defines the boundaries of your model. This concept is critical in large software projects. A Bounded Context sets the limits around what a specific team works on and helps them to define their own vocabulary within that particular context.

Take the example of a customer in retail. In one context, a customer is a person who buys products from a store. In another context, a customer is a person who a retailer markets its products to. The customer is the same but is in different bounded contexts, each of which act on the customer entity based on their own rules.

When you define a Bounded context, you define who uses it, how they use it, where it applies within a larger application context, and what it consists of in terms of things like Swagger documentation and code repositories.

This pattern was first described in [Evans](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software-ebook/dp/B00794TAUG)
