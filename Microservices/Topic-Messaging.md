Topic Messaging
===

Context: decoupling services through messaging

Problem: how do I decouple services with massive message traffic?

Solution: use an at-least-once message delivery system like Kafka. These systems scale very well, but service implementations need to be able to handle duplicate deliveries.
