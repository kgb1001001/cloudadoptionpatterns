# Asynchronous Replication

You are building a system that has data in multiple distributed locations.  You need to make sure that the data in those locations is consistent.

**How do you guaranteee that data is consistent across multiple instances of a scalable store, but at the same time keep from having to require that all transactions wait until the data is updated in all locations?**

Data can be replicated by transmitting changes that occur between transactional checkpoints. Often, data can have gaps and still be valid; data for analytical purposes (for example, user behavior metrics) can potentially miss minutes but still be valuable enough to serve as a source for information. Especially for this kind of data it is often not acceptable to wait for it to be safely replicated as this may put unacceptable delays on interactive user flows.

Therefore,

**Send data that can be lost or re-created in asynchronous batches to other datacenters, outside the scope of any transactions (either by using systems that forego transactions, or by sending the data after the transaction has been completed at the source). Messaging systems like [Kafka](https://kafka.apache.org/) can be helpful here to transport data between datacenters (“fire and forget”).**

Asynchronous replication will come at a cost: data will be lost if the source datacenter fails. There is no way around this: some transactions that have just been committed in the originating datacenter before it went down will not have propagated out of it. These transactions will be lost forever if we assume that the original datacenter is lost forever. This is the reason that this pattern stresses its usefulness for data that can be lost. Which data can be lost in the case of a datacenter outage (a very irregular event) is a business decision and therefore not in scope of this paper. An example may be a company that hosts weblogs: it may decide that, in case of a datacenter failover, losing some comments and posts is annoying to the user, but from a business perspective entirely acceptable.

If the business critically depends on certain data, then this data should not be replicated this way; [Synchronous Replication](Sync-Replication.md) should be used instead.

For instance, [MySQL](https://www.mysql.com/) has been wildly popular with large scale websites because of its built-in [asynchronous replication](https://dev.mysql.com/doc/refman/8.0/en/replication.html). Executed statements and/or row changes are written to a binary log on the *master* and can be fetched by *slaves*. The log is written on transaction commit and thus only available to slaves outside the transaction scope; this means that replication can cross unreliable network links without impacting the observed speed of on-line transactions against the master.

A lot of “eventually consistent” storage systems work by accepting writes at one node in the cluster, and then replicating it across multiple nodes so that eventually, a quorum of nodes agrees on the data. [Cassandra](http://cassandra.apache.org/) is a good example, because it can be operated to be aware of mutliple dataenter topologies. Data can be written to a local node of a datacenter-spanning cluster, and it will eventually arrive at nodes in other datacenters, asynchronously.
