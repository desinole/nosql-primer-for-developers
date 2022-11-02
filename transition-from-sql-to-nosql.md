[Back to Intro](intro.md)

# Transition from SQL to NoSQL

Some salient points to consider when transitioning from SQL to NoSQL:

- The question should not be "Should I use SQL or NoSQL?" but rather "What is the best fit for my application?". The answer usual is **Polyglot data**.
- When it comes to spinning up NoSQL clusters and managing them versus choosing NoSQL-as-a-Service, the latter is the way to go. It is much easier to manage and scale.

## Checklist for considering SQL versus NoSQL

It is important to ask yourself questions like:

- Is the system ok with sacrificing consistency for performance? Banking solutions are not ok with this.
- If I want to use NoSQL, does my data meet at least one of the 3Vs - volume, velocity, variety?

| | SQL | NoSQL |
|--------------|--------------|-----------|
| **Model** | Relational | Non-relational |
| **Storage** | Tables | JSON docs, Key-value pairs, column stores, graphs |
| **Data Properties** | Every record in table has same properties | Flexibility in properties varies across record |
| **Relationships** | Joins | Denormalization |
| **Schema** | Strict | Flexible |
| **Transactions** | ACID | Varies by solution |
| **Data Consistency** | Strong | Variable |
| **Scale** | Vertical | Horizontal |

## Total Cost of Ownership (TCO) of SQL versus NoSQL

![TCO](/img/tco.png)
*Caption: as-a-service solutions offer lower TCO*

NoSQL databases are by nature intended for distributed hosting. Question is do you want to host it yourself or farm off to a cloud or 3rd party provider. You should look at total cost of ownership (TCO) before making that decisions. Data residency requirements may require self hosting. Speed of development and time to market may require going with a cloud provider as-a-service.

## Consistency

![Consistency scale](/img/consistency.png)
*Caption: NoSQL systems offer either strong or eventual consistency and some provide a range*

Most relational systems are always strongly consistent. Most NoSQL systems make you pick between strong and eventual consistency. Some systems  creatively allow for middle ground between strong and eventual consistency.

## Latency

![Latency](/img/latency.png)
*Caption: For distributed databases latency is a major issue*

Latency is a function of the distance between the client and the server. The closer the client is to the server, the lower the latency. Latency is also a function of the number of hops between the client and the server. The fewer the hops, the lower the latency.

For distributed databases the important questions to answer are:

- How long do reads and writes take? Single or low double digit milliseconds is ideal
- What percentile (50? 90? 99?) of read-writes are the lowest latency?
- When you scale how long does it take for new instances to catch up?

## Throughput

![Throughput](/img/throughput.png)
*Caption: For distributed databases throughput is the currency of operation*

Distributed databases are similar to streaming services. The **speed** aka the throughput is extremely important to consider. In this case, throughput is the amount of items passing in and out of the system per second. In the case of databases, throughput is the sum of CRUD operations per second. Databases often have to pick throughput based on whether they are read heavy (generates historical reports) or write heavy (stores IoT telemetry).

## Partitioning choices

![Partitioning](/img/partitioning.png)
*Caption: For distributed databases data partitioning choices dictate performance*

Since data is stored on multiple nodes, choosing a decent partition key can determine long-term performance of the data and is often the most important design choice impacting performance.

## Geographical distribution

![Throughput](/img/geographical-distribution.png)
*Caption: For distributed databases handling geographical distribution is essential*

NoSQL databases are best suited for applications spanning large geographies, for instance, a global e-commerce system. Some essential questions to ask while provisioning these databases:

- How fast do these instances operate at full capacity?
- What is the read-write strategy for multiple instances?
- How do you handle data locality?
