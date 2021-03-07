Service Registry
===

You are building applications using a [Microservices Architecture](../Microservices/Microservices-Architecture). You have many different [Business Microservices](../Microservices/Business-Microservice.md) comprising your application.

**How do you decouple the physical location of a service instance from its clients so that the client code will not have to change if the address of the service changes?**

You don’t want to have to change client code each time you update a service, for instance, if you update the version of the service, which may change the URL
Likewise, You don’t want to have to hard-code the physical addresses of a service into client code – that would make it difficult, for instance, to move code between development and production when the physical addresses of the systems change.

When a system is stable, knowledge about the system is identical no matter where you look. The system has converged and is working at optimal efficiency. However, the more complex a system grows (in terms of the number of machines, the amount of services endpoints, etcetera), the more often changes will be made to it. With configuration systems that rely on (generated) files and application restarts, it will take a while for every change to propagate, and if this time is long enough and system changes are often enough, it is easy to see that the system potentially never converges. This leads to reduced availability, and therefore is economically unsound but also impacts the amount of “damage” a system can take before it becomes completely unavailable.

*Therefore,*

**Use a *Service Registry* to map between a unique identifier and the current address of a service instance in order to decouple the physical address of a service from the identifier. The Service Registry pattern was first introduced in [Daigneau](https://www.amazon.com/Service-Design-Patterns-Fundamental-Solutions/dp/032154420X) and remains useful in a microservices implementation – perhaps even more so given the number of individual services in a [Microservices Architecture](../Microservices/Microservices-Architecture.md).**

At its simplest, a Service Registry is just a repository for information about services. However, many implementations add other metadata about the service along with the physical address, such as a generic server name (useful when you have multiple instances of a service) and health information such as status or uptime.

A service registry takes care of quickly spreading new knowledge around the cluster and often only needs a handful of nodes in each datacenter to be resilient. Application APIs are available to actively inform application instances of configuration changes they would be interested in, so that applications can quickly respond; convergence therefore can take place in seconds instead of hours, greatly reducing the time tha the system is in a transitional state and thus minimizing the amount of time that the system has less than optimal resilience.

As the service registry should be *Topology Aware*, it need to be setup in a topology aware fashion itself; either only returning local references (this can easily be done with any system by running it separately per datacenter) or by returning local references by default and remote references when requested (this needs support in the service registry).

For example, [Consul](https://www.consul.io/docs/intro) is a service registry system that contains a large number of very desirable features. For example, it has a DNS interface which makes integrating applications a breeze, and it is based on the Raft consensus protocol which makes the code simple to verify and reason about [@raft]. Most important, though, is the way how Consul handles multiple datacenters.

Consul typically runs as a small daemon on every system. This makes a bootstrap process of “how do I find my service registry?” go away: it sits on *localhost* at well-known ports. Only a handful of nodes participate in the consensus algorithms, they are called “servers” and usually they are run on dedicated machines. Within a datacenter, the servers use Raft to elect a leader among them, and this leader receives all queries; node-local Consul agents are configured with one or more bootstrap nodes and then join a gossip network to replicate the state of the network (who are the members, where are the members, and who is the leader).

Optionally, Consul can join multiple clusters by so-called WAN bridges. This, in effect, creates a new gossip network between the servers over the WAN, enabling services in one datacenter to forward queries to another datacenter when the queries cannot be locally resolved; for example, this is the case when a client explicitly requests a service lookup in a remote datacenter. There is also support for enumerating known datacenters and nodes in each datacenter, so that it is possible for subsystems that need it to gain complete knowledge of the configuration at a given point in time; this can be used for example to configure high availability clusters automatically, based on the location of available participants in the cluster.

Other examples of Service Registries include [Netflix Eureka](https://dzone.com/articles/netflix-eureka-discovery-microservice) and the [Kubernetes API server](https://kubernetes.io/docs/reference/command-line-tools-reference/kube-apiserver/).

Not all projects will require a Services Registry – if you have only a handful of services in your application then the setup and management of the registry infrastructure is often more trouble than it’s worth. But if you have more than a half a dozen services then it may become useful when alternative ways of managing service location (such as configuration files) become cumbersome.
