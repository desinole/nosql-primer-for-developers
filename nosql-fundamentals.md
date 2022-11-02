[Back to Intro](intro.md)

# NoSQL Fundamentals

- CAP Theorem
- 3V's of Big Data

## CAP Theorem

### CAP Theorem - Pick 2 of 3

![CAP Theorem](/img/cap-theorem.png)
*Caption: Consistency, Availability, Partition Tolerance - pick 2 of 3*

Due to physics, Consistency of data becomes a matter of trade-off in NoSQL databases. Like all distributed systems, NoSQL databases are subject to the CAP Theorem also named Brewer's theorem, which states that it is impossible for a distributed data store to simultaneously provide more than two out of the following three guarantees:

- Consistency: Every read receives the most recent write or an error
- Availability: Every request receives a (non-error) response – without the guarantee that it contains the most recent write
- Partition Tolerance: The system continues to operate despite an arbitrary number of messages being dropped (or delayed) by the network between nodes

### PACELC Theorem

> Partitioning (P) in a distributed computer system, one must choose between availability (A) and consistency (C), but else (E), even when the system is running normally in the absence of partitions, one has to choose between latency (L) and consistency (C)

The CAP theorem implies that in the presence of a network partition, we must choose between consistency and availability. Given that networks are not completely reliable, we must tolerate partitions in a distributed system. Fortunately, though, we get to choose the tradeoffs when a partition does occur. This is known as the **PACELC theorem** which states: in case of network partitioning (P) in a distributed computer system, one must choose between availability (A) and consistency (C, but else (E), even when the system is running normally in the absence of partitions, one has to choose between latency (L) and consistency (C).

![Sacrifice Availability for Consistency](/img/sacrifice-availability.png)
*Caption: Sacrifice Availability for Consistency*

![Sacrifice Consistency for Availability](/img/sacrifice-consistency.png)
*Caption: Sacrifice Consistency for Availability*

In this scenario, the system has updated one node successfully, but before updating the second node, the system experienced a network partition. In order to provide consistency aka, read retrieves the latest write, if the system is unable to access the nodes with the new data due to network partitioning, it returns an error.

In this scenario, the system has updated one node successfully, but before updating the second node, the system experienced a network partition. In order to be available aka, read retrieves a value, even if it is stale, if the system is unable to access the nodes with the new data due to network partitioning, it returns an error. In addition, the system can continue storing writes, even during the network partitions and process these writes later when the partition condition no longer exists.

### 3V's of Big Data

![3V's of Big Data](/img/3v.png)
*Caption: 3V's of Big Data - volume, velocity, variety*

Discussing NoSQL requires a discussion on the 3Vs of big data – Volume, Velocity and Variety.

The term big data leads us to believe the only criteria for a dataset to be classified under this category if for the dataset to be massive i.e. volume. Large volumes of data, particularly datasets measured in terabytes or petabytes, present unique challenges in terms of storage and processing. Additionally, search algorithms which might work on smaller datasets, may not operate as efficiently for these massive datasets.

Velocity and variety are other aspects of big data. Velocity refers to the speed of incoming data and the challenges presented by such data in terms of storage and processing. The use case for data velocity becomes apparent in real-time systems – systems which require data to be collected and processed instantaneously, for instance, self-driving vehicles. High-velocity data can present challenges in terms of testing the upper limits of responsiveness of the hardware its stored on. Also, analytical algorithms, in general run for longer periods, which may not be sufficient for the type of real-time response these types of systems expect.

Variety refers to a diversity of data types/formats – tabular, photo, video, audio, in addition to data from a wide variety of sources such as social media, mobile, sensors. Relational databases are not designed to handle storage and processing such different types/formats of data, because they cannot be easily stored and retrieved from tables in the form of rows and columns, or, be operated on by SQL queries and joins.
