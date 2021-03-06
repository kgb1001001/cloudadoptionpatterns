Service Registry
===

You are building applications using a [Microservices
Architecture](). You have many different [Business Microservices](../Microservices/Business-Microservice.md)
comprising your application.

**Problem:** How do you decouple the physical address (IP address) of a
microservice instance from its clients so that the client code will not
have to change if the address of the service changes?

**Forces:**

-   You don’t want to have to change client code each time you update a
    microservice, for instance, if you update the version of the
    microservice, which may change the URL

-   You don’t want to have to hard-code the physical addresses of a
    microservice into client code – that would make it difficult, for
    instance, to move code between development and production when the
    physical addresses of the systems change.

**Solution:** Use a *Service Registry* to map between a unique
identifier and the current address of a service instance in order to
decouple the physical address of a service from the identifier. The
Service Registry pattern was first introduced in \[Daigneau\] and
remains useful in a microservices implementation – perhaps even more so
given the number of individual services in a *Microservices
Architecture*.

At its simplest, a Service Registry is just a repository for information
about services. However, many implementations add other metadata about
the service along with the physical address, such as a generic server
name (useful when you have multiple instances of a service) and health
information such as status or uptime.

Examples include IBM Bluemix’s Service Discovery, Netflix Eureka and the
Amalgam8 Registry.

**Results:** Not all microservices projects will require a Services
Registry – if you have only a handful of services in your application
then the setup and management of the registry infrastructure is often
more trouble than it’s worth. But if you have more than a half a dozen
services then it may become useful when alternative ways of managing
service location (such as configuration files) become cumbersome.
