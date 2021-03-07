Synchronous Replication
===

Some data is important enough not to lose. It can represent a transaction, or data that the system cannot recreate (because it originates externally, for example it came in through an API). Often, the data carries a monetary value or an external obligation.

**How do you guarantee that data is never lost when building a distributed cloud-based system?**

Outages of any kind come with losses. Preventing or reducing the cost of these losses costs money, so these measures can be seen as an insurance premium. It is important to make a quick calculation of costs of loss and benefits of prevention of loss, but sometimes the balance will be that data cannot be lost even under very rare circumstances. This means that transactions need to span multiple datacenters to insure against losing data that is in-flight in a datacenter when it goes down.

*Therefore,*

**Replicate data between datacenters synchronously when loss of data is deemed costly. Synchronous replication can severely impact the responsiveness of systems, but is an essential tool. In effect, the transaction should not complete until the data has landed in a quorum subset of the systems involved. Doing quorum writes obviously reduces availability, so whenever synchronous replication is involved there is a need to make sure that transactions are re-tried.**

Synchronous replication is a measure of last resort. It is expensive, slows systems down, has the risk of reduced availability, and forces applications to be aware of all that. An application that uses a local MySQL master cluster that asynchronously replicates to another data center can be blissfully unaware of that happening–for all practical purposes, the database behaves like this replication isn’t happening and therefore behaves like a single local instance. When synchronous replication becomes part of the picture, however, a single transaction will become much slower (because of the round trip times involved), has a higher risk of failing (because of network connectivity issues), and thus the application should be written to take this into account. Often, attempts to hide this complexity in a library fail as business logic needs to be adapted to handle new kinds of failures; this increase in business logic complexity puts a premium on synchronous replication.

If there is any way that the system can get away with asynchronous replication, that should be the preference. The cost of losing a couple of in-flight transactions in a once-a-year event should be clearly weighted against the overhead of adding synchronous replication.

For example, [Cassandra](https://cassandra.apache.org/) is an elastic [Key-Value Store](Key-Value-Store.md) that has the interesting property of being datacenter aware. Cassandra nodes can be tagged with a datacenter (or even a rack) name, and the system can be instructed to replicate data across datacenters. With strong write consistency, Cassandra won’t complete a write operation until at least a quorum of all datacenters have reported back that the write has been written to disk. In this sense, one can be safe that when Cassandra reports back that a write was successful, the data has been durably stored in multiple datacenters.

One drawback of Cassandra is that writes are atomic operations, but there is no locking. This means that conflicting writes are possible. There are ways to lessen the impact of conflicting writes which are out of scope of this pattern as they are very Cassandra-specific, but generally speaking conflicting writes are bad and should be avoided.

The way to avoid conflicting writes is to serialize them. A good way to do this is to use [Global Locks](/Global-Locks.md) around the operation. The lock assures serialized writes; a read-before-write in the lock will detect write conflicts, and Cassandra will assure replication across datacenters.

