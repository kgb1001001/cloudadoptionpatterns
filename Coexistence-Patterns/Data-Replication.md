# Data Replication

You are following a [Cloud Refactoring]() strategy using the [Strangler Application]() and you find the need to slowly refactor a database over time so that each [Business Microservice]() can in the end own its own data.  However, since this process may take months or even years, you will find yourself in the situation where you have different clients that are querying and updating the data in the original, monolithic database, and also the data in the individual distributed databases for each microservice.

**How do you keep the data synchronized between the two different sets of databases?**

The problem with trying to keep two different databases (especially those that are implemented in different technologies) is that 

**Employ a Data Replication approach that updates both sets of databases whenever one changes.**

Data Replication is a strategy that can work in a couple of different approaches, but which approach you choose depends on the particular situation you find yourself in.  In situations where data cannot ever be different between the two databases, a Synchronous Replication approach is often the best.  However, all Synchronous replication approaches share the same drawback - they increase the time it takes to finish any update transaction on either database, since you have to wait until you receive confirmation of the update on the target database before the transaction can complete on the original database.  What's more, most synchronous approaches are going to be technology-specific, that is, you will have to choose a replication tool that supports your particular database.  So, for instance, if you want to replicate part of an Oracle database to another Oracle database,  you would use Oracle GoldenGate to provide real-time synchronous replication. 

Asynchronous replication schemes have the advantage that they can be more flexible in how you manage the data transformation between the origin and target database.  For instance, Change Data Capture approaches allow you to route the change logs (expressed as Events) from the origin to to multiple different receivers that could transform that data into their own target format.