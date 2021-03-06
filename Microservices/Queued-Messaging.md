Queued Messaging
===

Context: decoupling services through messaging

Problem: how do I decouple services without losing too much of the current (transactional) properties?

Solution: use an exactly-once message delivery system like RabbitMQ or ActiveMQ. These systems don't scale as well as those with more relaxed properties, but have the least impact on business logic/service internals.
