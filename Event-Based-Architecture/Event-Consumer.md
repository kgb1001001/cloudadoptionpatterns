You are building a Microservices Architecture and you need to decouple one microservice from another

How do you allow a microservice to find out when data belonging to another microservice changes without constantly querying the microservice API?

Declare your microservice as an Event Consumer that can listen in on an event that indicates that a fact has occurred that it is interested in.

Event consumers are the recipients of the diverse events they may have indicated a preference for. A sophisticated RA for event driven architecture will cater to the existence of diverse types of consumer that are capable of receiving events of varying degrees of complexity, throughputs, technologies and technical  maturity.
