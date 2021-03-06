Global Locks
===

There are various circumstances where work needs to be coordinated
between datacenters. An example could be seen in the previous section,
where <span><span style="font-variant:small-caps;">Synchronous
Replication</span></span> in an otherwise transaction-less key/value
store could result in write conflicts; another example is where a single
process should work on data and the process should only be started in
(potentially) a different datacenter when the original one goes down.
Coordination can also mean turning an asynchronous system into a
synchronous one by waiting until the replication has happened;
preferably, other systems shouldn’t be writing at that time.

*Therefore,*

Have a system to implement locking across datacenters. With these global
locks, it becomes possible to coordinate systems and actions between
datacenters. A transaction can be scoped by taking a lock; writes to
otherwise transaction-less systems can then be serialized on the lock. A
single process to do work can be elected similarly: one process holds a
long-running lock, and when it fails, the lock is released and other
processes then have a chance to obtain it and start performing work.

Like synchronous replication, locking across datacenters is expensive
and not transparent to the locking process. Locks can fail, they take
some time to obtain as they must be coordinated with instances of the
locking system running in multiple datacenters, and the name or key to
lock on must be chosen carefully to balance between locking contention
(lock names too coarse grained) and risk of conflicts (lock names too
fine grained). It’s a tool in the distributed system designer’s toolbox,
but not one that should be retrieved at the first hint that it might
solve a problem.

Example
-------

Zookeeper [@Zookeeper:online] is a distributed consensus system
originally implemented by YaHoo! to coordinate their massive (for that
time) networks. YaHoo! wrote the system to perform leader election,
locking, and to act as a service registry. It has been around for a long
time and can be considered battle-hardened, and it performs very well as
a global locking service.

One way to run Zookeeper is to have 5 nodes over <span><span
style="font-variant:small-caps;">Three Datacenters</span></span>.
Zookeeper does not benefit from more machines (as the leader of the
cluster is the bottleneck), and in this way the outage of any datacenter
will leave a quorum intact; furthermore, two machines in different
datacenters can go down with no impact. This is a general pattern for
data replication that is applicable to replicated systems like Cassandra
and Kafka as well; contrary to datacenter outages, machine outages are
common, and with a 3 node setup a single node failure would immediately
put the system at risk of not being available.

Interacting with Zookeeper is quite low level and requires a lot of
knowledge on how the various primitives are implemented; in essence, it
is more a toolbox than an end-user application. Various users have
published “recipes” for interacting with Zookeeper in library form, and
their use is recommended–Apache Curator [@Apach72:online] is a leading
software component in this field.

