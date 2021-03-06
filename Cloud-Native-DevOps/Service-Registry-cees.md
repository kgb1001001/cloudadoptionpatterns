[//]: # (This is the version from Cees' paper, should be merged with Kyle's)

Service Registry
===

When clusters and subsystems live in various datacenters, it becomes
hard to keep track of what lives where. The old-fashioned method of
keeping hostnames in configuration files becomes problematic.

Even when you <span><span
style="font-variant:small-caps;">Automate</span></span>, it is still
hard to have configuration files reflect the state of a whole network,
especially with machines going away in far-away datacenters. There are
ways to circumvent this, for example by very often re-generating
configuration files from dynamic state, but this still brings delays in
spreading configuration knowledge that may impact system performance.

*Therefore,*

Use a Service Registry to keep an up-to-date view of which (instances
of) services are available and where they live. It is helpful if the
registry is <span><span style="font-variant:small-caps;">Topology
Aware</span></span>. Some candidates are Consul [@Consul:online],
Zookeeper [@Zookeeper:online] and etcd [@etcd:online].

Discussion
----------

When a system is stable, knowledge about the system is identical no
matter where you look. The system has converged and is working at
optimal efficiency. However, the more complex a system grows (in terms
of the number of machines, the amount of services endpoints, etcetera),
the more often changes will be made to it. With configuration systems
that rely on (generated) files and application restarts, it will take a
while for every change to propagate, and if this time is long enough and
system changes are often enough, it is easy to see that the system
potentially never converges. This leads to reduced availability, and
therefore is economically unsound but also impacts the amount of
“damage” a system can take before it becomes completely unavailable.

A service registry takes care of quickly spreading new knowledge around
the cluster and often only needs a handful of nodes in each datacenter
to be resilient. Application APIs are available to actively inform
application instances of configuration changes they would be interested
in, so that applications can quickly respond; convergence therefore can
take place in seconds instead of hours, greatly reducing the time that
the system is in a transitional state and thus minimizing the amount of
time that the system has less than optimal resilience.

As the service registry should be <span><span
style="font-variant:small-caps;">Topology Aware</span></span>, it needs
to be setup in a topology aware fashion itself; either only returning
local references (this can easily be done with any system by running it
separately per datacenter) or by returning local references by default
and remote references when requested (this needs support in the service
registry).

Example
-------

Consul is a service registry system that contains a large number of very
desirable features. For example, it has a DNS interface which makes
integrating applications a breeze, and it is based on the Raft consensus
protocol which makes the code simple to verify and reason about [@raft].
Most important, though, is the way how Consul handles multiple
datacenters.

Consul typically runs as a small daemon on every system. This makes a
bootstrap process of “how do I find my service registry?” go away: it
sits on <span>localhost</span> at well-known ports. Only a handful of
nodes participate in the consensus algorithms, they are called “servers”
and usually they are run on dedicated machines. Within a datacenter, the
servers use Raft to elect a leader among them, and this leader receives
all queries; node-local Consul agents are configured with one or more
bootstrap nodes and then join a gossip network to replicate the state of
the network (who are the members, where are the members, and who is the
leader).

Optionally, Consul can join multiple clusters by so-called WAN bridges.
This, in effect, creates a new gossip network between the servers over
the WAN, enabling services in one datacenter to forward queries to
another datacenter when the queries cannot be locally resolved; for
example, this is the case when a client explicitly requests a service
lookup in a remote datacenter. There is also support for enumerating
known datacenters and nodes in each datacenter, so that it is possible
for subsystems that need it to gain complete knowledge of the
configuration at a given point in time; this can be used for example to
configure high availability clusters automatically, based on the
location of available participants in the cluster.

In essence, Consul provides all the functionality that is needed to be
<span><span style="font-variant:small-caps;">Topology
Aware</span></span>, which makes it a very good fit for these kind of
systems.
