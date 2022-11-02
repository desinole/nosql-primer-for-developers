[Back to Intro](intro.md)

# Types of NoSQL databases

- Key-Value
- Document
- Graph
- Column-oriented
- Multi-Model

<mark>**Note: [Dbdb.io](https://Dbdb.io) is a great resource to compare different databases.**</mark>

## Key-Value databases

![Example of records in a key-value database](/img/key-value.png)
*Caption: Example of records in a key-value database*

Data is inserted as key-value pairs and retrieved using the key. This type of lookup using keys is a O(1) lookup. The partition key, in addition to the record key enables the fast lookups.

The data is schema-less and can often store most primitive data types, JSON and even blobs in certain cases. The key value type basically, uses a hash table in which there exists a unique key and a pointer to an item of data. The data is generally stored on high-performing volatile memory (RAM) or solid-state drives (SSD).

The simplicity of this scales well but it can limit the complexity of the queries. It lacks the sophistication of relational databases or even other models of NoSQL databases. As the volume of data increases, the generation and maintenance of keys becomes more complex.

Some examples of Key-Value NoSQL databases: Dynamo, MemcacheDB, Redis, Riak and Azure Table Storage.

## Document databases

![Example of records in a document database](/img/document.png)
*Caption: Example of records in a document database*

Document-oriented databases store data in the form of documents which encapsulate and encode data in some standard formats or encodings like XML, YAML, JSON, BSON. Each document can be accessed using a unique key like a key-value store. However, documented-oriented databases usually also offer an API or query language to query and retrieves documents.

The schema is often referred to as loose schema or schema-free. Documents embed attribute metadata associated with stored content, which provides a way to query the data based on the contents.

For instance, in the above example, one could search for all documents in which "Location" is "Orlando" and this query would deliver a result set containing all documents associated with that city.

Some examples of Document-oriented NoSQL databases: Apache CouchDB, RavenDB, MongoDB, OrientDB, Azure Cosmos DB SQL API.

## Graph databases

![Example of records in a graph database](/img/graph.png)
*Caption: Example of records in a graph database*

Data in real world is naturally connected. Traditional data modeling focuses on entities. Graph databases model the rich relationships between entities by allowing you to model both entities and relationships naturally.

Graph databases are composed of vertices (nodes) and edges. Vertices or Nodes denote discrete objects such as a person, a place, or an event. Edges denote relationships between vertices

Some examples of Graph NoSQL databases: Neo4j, InfiniteGraph, Azure Cosmos DB Graph API.

## Column-oriented databases

![Example of records in a column database](/img/column.png)
*Caption: Example of records in a column database*

Column-oriented aka wide-column stores such as Cassandra and HBase are optimized for queries over large datasets, and store columns of data together, instead of rows. 

The illustrations below show a simple example of how data is usually represented in relational databases versus how data is split up and stored by columns in column-oriented databases.

Column-oriented databases, serialize all the values of a particular column together. A column in a column-oriented database is the equivalent of a row in a relational database. Entire columns are stored and retrieved together which makes aggregation, sorting and range operations on large datasets are extremely fast since the values are stored together. Also, since the data types are the same, compression of stored data is easier. 

Some examples of column-oriented NoSQL databases: Apache Cassandra, HBase, Azure Cosmos DB Cassandra API.

## Multi-model databases

The past decade with the rise of the cloud has seen an explosion in databases that support multiple models, not just one. A multi-model database is a database management system designed to support multiple data models.

Multi-model databases are polyglot - Document, graph, relational, and key–value models are examples of data models that may be supported by a multi-model database. Single integrated backend means similar operations for setup, maintenance and security (Authentication/authorization). While there are specialized multi-model databases like Cosmos DB, most database systems are organically becoming multi-model. For instance, SQL server can store data as text, XML, JSON and so on

Some examples of multi-model databases are Azure Cosmos DB, OrientDB, Arango DB and so on.
