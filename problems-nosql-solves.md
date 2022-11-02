[Back to Intro](intro.md)

# What problems do NoSQL systems solve?

Largely NoSQL databases solve

- Impedance mismatch
- Scaling issues

## Impedance Mismatch

### The Problem

![Impedance Mismatch](/img/impedance.png)
*Caption: 1 record across 3 tables and 6 different rows*

In this case, to write one User object, using database normalization techniques, we write the data across 6 different rows in 3 different tables. Similarly, to read a User record, we would have to read 6 rows spread across 3 tables. Now this was a simple example.

In even moderately complex systems, read or write operations for the object could easily involve dozens of tables. This read-write by disassembling and reassembling is inefficient and manifests itself in higher resource consumption. Object-Relational Mapper (ORM) frameworks are supposed to address this exact problem but have the side effect of reduced speeds due to translation of queries.

### Solving Impedance Mismatch with NoSQL

![Eliminate Impedance Mismatch](/img/eliminate-impedance-mismatch.png)
*Caption: store the record as a single JSON document*

In comparison, by employing a documented-oriented NoSQL database instead of a relational database, the same object is stored as a JSON document.

This method of storage:

- Eliminates the object-relational impedance because reads and writes involves single JSON documents for each object
- Simplifies application development since disassembling and reassembling of objects are no longer required
- No ORM frameworks are required

## Scaling Issues

### Vertical Scaling causes severe constraints

![Eliminate Impedance Mismatch](/img/vertical.png)
*Caption: vertical scale systems hit constraints early*

Database systems must be able to scale to match peak system loads i.e. total number of concurrent connections.

Traditional methods of scaling involve increasing your system hardware, aka, scale up to meet system load. This approach is fraught with issues like upper bound on hardware specifications and the server as a single point-of-failure.

### NoSQL system scale horizontally

![Eliminate Impedance Mismatch](/img/horizontal.png)
*Caption: horizontal systems can hypothetically keep scaling*

NoSQL databases, on the other hand, are designed to store data and distribute load across multiple nodes. These nodes are usually commodity hardware optimized to perform for data up to certain sizes (10GB, for instance). 

As the application load increases, the system keeps adding nodes i.e. scaling horizontally. The added benefit to this type of architecture is that when individual node(s) fail, the non-failing nodes can keep responding, which greatly reduces the single point-of-failure risk for NoSQL databases. This type of behavior greatly enhances the availability of the database system and allows the system to maintain steady performance regardless of scale of data stored or concurrent connections requesting this data.

However, this gain in availability comes as the risk of violating relational database ACID (atomicity consistency isolation durability) principles.
