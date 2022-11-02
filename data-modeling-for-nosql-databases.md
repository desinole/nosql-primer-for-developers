[Back to Intro](intro.md)

# Data modeling for NoSQL databases

- Schema-free data
- Denormalization

One of the key features of the JSON documents stored using the SQL API is the lack of adherence to a rigid schema. This type of data is called schema-less data. 
We will talk about why database joins in relational databases are expensive and how to address that with denormalization.
And finally we will talk about modeling relationships – many-to-many, one-to-many and so on

## Schema-free data

![Example of schema-free data](/img/schema-free.png)
*Caption: Example of schema-free data*

Schema-free data aka loose schema indicates a lack of strict adherence to a particular schema. Data might be similar but not same. Caveat: resist throwing completely disparate schema together because it messes with items like partition keys which will determine performance. Schema-free data reflects real life where you can get data from multiple sources

## Denormalization

### Why data normalization is expensive?

![Why data normalization is expensive - joins](/img/Denormalization-normalization.png)
*Caption: Why data normalization is expensive - joins*

In relational design, significant focus is placed around describing the entity and its relation to other entities first. After the relations are finalized, items impacting performance like indexes are designed later. When the schema is normalized, data redundancy is reduced, and storage becomes more efficient.

Finally, queries with joins bring the data back together again. However, joins cause bottlenecks on read, and this model does not scale horizontally.With joins, there is no O(1) complexity because the process of joining tables does not involve any kind of hash table style lookups. Joins also afford no O(n) complexity, O(n) is not a join, it's a filter. Most joins will happen on indexed columns, it will be O(m log n).

Joins are often plagued by issues like the design not accounting for null values and the lack of or incorrectly configured indexes in the database or null values in index fields – which are allowed. Disk I/O can also cause a significant impact on join operations. Joins can increase random seeks especially if we're jumping around reading small parts of a large table.

Since joins can be inefficient, particularly at scale, we attempt to denormalize this data using data modeling practices.

### One-to-many relationships

![Denormalization - handling one-to-many relationships](/img/Denormalization-one-to-many.png)
*Caption: Denormalization - handling one-to-many relationships*

Modeling one-to-many is straightforward. Embed child records as array in parent records. For instance, states array is embedded in parent country document.

### Many-to-many relationships

![Denormalization - handling many-to-many relationships](/img/Denormalization-many-to-many.png)
*Caption: Denormalization - handling many-to-many relationships*

Denormalization involving many-to-many records involves more careful consideration. In the above example, Students have many-to-many relationship with Courses. So, a student may have multiple courses and a course may have multiple students.

### Embedding vs Referencing

![Embedding relationships](/img/Denormalization-embedding.png)
*Caption: Embedding relationships*

In this method, we select one of the entities as the parent document and embed an array of instances of the other entity. The many-to-many relationship means that some of the embedded instance will be repeated across different parent document, i.e., redundant data across records.

The advantage of this approach is that a single document contains all the data associated with the parent document which makes data retrieval a single operation.

The disadvantage with this approach is that since embedded data is repeated across parent documents, any updates to any child document would be an order of magnitude in operation cost compared to the relational model

This is often used for fairly static data like profile data or product listing info.

![Referencing relationships](/img/Denormalization-referencing.png)
*Caption: Referencing relationships*

In this method, we select one of the entities as the parent document and embed an array of references. This approach requires that the parent document and the related entities to be stored as separate documents in the database and use an approach like primary key-foreign key to perform the referencing.

This method is used when data is frequently changing and the parent document is not the only document that needs to be updated.