# Event Topic Registry
Event producers and consumers are expected to be decoupled, yet they have a shared interest in certain aspects of events and event messages. 

Given an underlying EDA assumption that event producers will not directly interact with or interrogate event producers about events and event messages, some means is required for that information to be shared.  Access to metadata is also important for prospective event producers.  If a new process or context is associated with occurrences of something of interest, then it may become an event producer.  Event metadata is needed to be able to publish events of the correct "type" to the correct topic.

Events do not exist in a vacuum.  At some point in the lifecycle someone has performed analysis to identify things that occur that are of interest beyond the scope of the occurrences themselves.  Identification of these scenarios involves several things: identifying candidate sources of those occurrences, candidate interested parties, candidate data that characterizes the occurrence and potentially additional candidate secondary data that is associated with the occurrences.

The event producer generates events of a specific event type known to the producer. Event consumers can consume events of a specific type known to them.  The loose coupling nature of event producers and event consumers and the events types which are involved does not allow for event processing to directly occur.  Between the event producer and the event consumer, there is not enough information that is shared to perform event generation and consumption.   

**How do we decouple the event consumers and producers while allowing them to find each other to share metadata?**

There are several issues that make this decoupling difficult:

+	How to identify the essential (required) and non-essential (optional) metadata attributes for events, event topics and event types/messages
+	How to structure the metadata associated with event types and event topics
+	Where to deploy an event registry and how event producers and consumers should locate it.
+	Agreeing on a standard interface to the event topic registry
+	Ownership over an event topic registry
+	Trustworthiness of event topic registry contents
+	Normative guidance about how many event types should be associated with an event topic.  Multiple event types per topic are likely to create an overly complex scenario.

Therefore,

**Create a registry to  publish metadata about events that a producer will emit.  The registry allows an event consumer to find and subscribe to those events, and then understand and utilize the information found in event messages.**

Although a key principle for Event Driven Architecture is decoupling of event producer and event consumer, there is never the less some essential information that needs to be shared between them.  The event registry allows this sharing to take place, but in a very indirect and decoupled manner.  Similar to a service registry, an event registry contains metadata about events that is needed by both the event producer and event consumer.

The Event Registry pattern has three participants:

1. Event Registry 
2. Event Producer 
3. Event Consumer 

Candidate metadata for the registry can include:

+	event type name 
+	event topic name 
+	event type schema (note: subtypes are possible) 
+	purpose of event type or event topic - why the event is interesting (still being discussed as to whether purpose should be associated with an event type of an event topic) 
+	event topic (which 0..n event producers will publish to, and which 0..n event consumers will subscribe to) 
+	additional information that could be descriptive of event context 
+	additional information that could be descriptive of the event producer (there could in theory be several producers of the same or similar event, and in some scenarios one might be considered to be of more interest than another, while in another scenario it might be appropriate to subscribe to events from several producers) 
+	additional information that could be descriptive of event lifecycle (e.g. how long should an even message be considered valid or current, how long would an event message instance be retained in an event store) 
+	additional information that could be descriptive of nonfunctional requirement or quality of service aspects 
+	additional information that might associate this event with a complex event pattern (or disassociate it from such a pattern) 
+	additional information that might be descriptive of "out of band information" associated with an event (i.e. information that is pertinent to the event but is not included in the event message) 

An *Event Topic Registry* can be thought of as a subtype of a Services Registry, in that the subscribers of the Events are similarly dependent upon the schema of the information forwarded to them on the topics as Service Consumers are upon the schemas provided by Services. 
