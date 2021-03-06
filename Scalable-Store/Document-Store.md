Document Store
===

You are building applications with a Microservices
Architecture. You are using RESTful API’s and representing the contents
of your HTTP requests and responses as JSON (Javascript Object Notation)
documents.

**How do you most efficiently store and retrieve the data
corresponding to your HTTP responses?**

-   You don’t want to have to translate the on-the-wire representation
    of an entity into another form just to store it in a database.

-   You want to build your solution quickly, and don’t want to have to
    add lots of additional libraries or code to manipulate a database.

**Store your JSON documents in a data store that is designed
to quickly and efficiently retrieve and store JSON documents – a
Document Store.**

In a microservice, the requests and responses that for the values
accepted and returned by the microservice are most commonly presented as
JSON values. JSON has emerged as the lingua-franca of REST, quickly
eclipsing and replacing XML for most service schemas. When a resource is
thus represented naturally by a JSON document developers want to use the
most efficient database they can for storing and retrieving that
information. Increasingly, this choice is a Document Store such as
MongoDB or CouchDB.

For instance, in MongoDB the basic construct is a collection of JSON
documents – and adding a JSON document to that collection is as simple
as obtaining a reference to the collection and calling an add method.
This type of simplicity is what makes this approach attractive to
developers building microservices in Javascript.
