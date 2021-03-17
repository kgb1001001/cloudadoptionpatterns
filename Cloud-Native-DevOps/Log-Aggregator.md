Log Aggregator
===

You are building applications using a [Microservices Architecture](../Microservices/Microservices-Architecture.md) and need to be able to debug problems that cross the different components of that architecture.

**How can you effectively view and search all of the different log files that emerge from all of the different distributed runtimes that comprise your collection of microservices?**

-   A *Microservices Architecture* can span dozens or even hundreds of individual application server processes. This results in hundreds of individual log files.

-   Microservices are often (but not always) implemented using cloud solutions that limit the lifetimes of the individual application server processes. When you use a solution like Cloud Foundry or docker, when an individual server container dies, any in-memory state within that cont ainer is lost.

Therefore,

**Use a *Log Aggregator* that pulls all of the files together into a single location. The Log Aggregator will “listen for” or tail each individual log file and forward the log entries to an aggregated collection point as they are made.**

Examples of Log Aggregators include: Splunk, Logstash, and the Cloud Foundry Loggregator.

Once you have collected log entries together, then the database of the entries can be searched in order to make debugging more meaningful. For instance, you can look for occurrences of the same log entry, perhaps a particular error message across multiple log files from multiple servers in order to see if a problem is sporadic or widespread.  This means you need a [Query Engine](Query-Engine.md) to be able to search the set of logs.

But the most helpful debugging approach is to take entries that are connected by a single thread of control that spans multiple microservices and correlate them together to find problems that cross a network of microservices in a particular call graph. That problem can be solved through the combination of a *Log Aggregator* and [Correlation ID’s](Correlation-ID.md).
