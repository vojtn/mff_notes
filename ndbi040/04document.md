| [Previous chapter](./03KeyValue.md) | [Overview](README.md) | [Next chapter](./05widecolumn.md) |
| - | - | - |


# Document-Oriented & Semi-Structured Data

## Document stores
* Documents are self-describing hierarchical structures (aggregates)
* Documents are typically grouped into collections
* Natural representation of application objects
* **Flexible schema:** Fields may differ between documents
* **Basic operations:** Insert/delete a document, retrieve documents by query, update document fields
* **Capabilities:** Rich query capabilities, but complex joins are not typical
* **Examples:** MongoDB, ArangoDB, CouchDB, RavenDB

## XML
Tree-structured document format
- Tag-based representation
- Supports attributes and nested
elements
- Designed for document exchange and
interoperability
- Strong ecosystem (XSD, XPath, XQuery)
older XML databases
```xml
<user id="42">
    <name>Alice</name>
    <email>alice@example.com</email>
    <roles>
        <role>admin</role>
        <role>editor</role>
    </roles>
</user>
```

## JSON
Lightweight hierarchical data format
- Based on key–value pairs and arrays
- Designed for data interchange in
web applications
- Native to JavaScript and widely used
in APIs
native for document databases
```json
{
    "id": 42,
    "name": "Alice",
    "email": "alice@example.com",
    "roles": ["admin", "editor"]
}
```


## Use Cases for Document Stores
* Event logging
* Content management systems (CMS) and blogging platforms
* Web analytics or real-time analytics
* E-commerce applications

## Data Modeling
* **Query-driven modeling:** Document design should reflect dominant application queries. 
* **Main decision:** Embed vs. Reference. The document schema is not arbitrary; it is shaped by access patterns.

## Schema-on-Write vs Schema-on-Read
Schema-on-write: structure first → then store data  
Schema-on-read: store data first → interpret structure later

## MongoDB
* Initial release: 2009 (Written in C++, Open-source, Cross-platform)
* Uses JSON documents with dynamic schemas (no enforced structure)
* **Key Features:** High performance (indexes), High availability (replication, automatic failover, eventual consistency), Automatic scaling (sharding), MapReduce support.

### Terminology & Structure
* Each instance has multiple **databases** → Each database has multiple **collections** → Collections store **documents**.
* **Documents:** Written in JSON, stored as BSON.
* **BSON (Binary JSON):** Binary-encoded serialization. Allows embedding of documents, arrays, and extra types (e.g., date). Designed for efficient storage and fast traversal.
* **Document Limits & Rules:** * Max size: 16MB (prevents using too much RAM). GridFS tool divides larger files.
    * `_id` is reserved as a primary key, unique in the collection, immutable, cannot be an array.
    * Field names cannot start with the `$` character.

### Documents
Uses JSON
- Stored as BSON
- Binary representation of JSON
- Have maximum size: 16MB (in BSON)
- Not to use too much RAM
- GridFS tool divides larger files into fragments
- Restrictions on field names:
- _id is reserved for use as a primary key
- Unique in the collection
- Immutable
- Any type other than an array
- The field names cannot start with the $ character


#### BSON (Binary JSON)
Binary-encoded serialization of JSON documents
- Allows embedding of documents, arrays, JSON simple data types + other
types (e.g., date)
- Purpose
- efficient storage
- fast traversal of documents

### References
Including links / references from
one document to another
- More flexibility than embedding

Disadvantages:
- Can require more roundtrips to the server (follow up queries)

Use when
- data chenges freuquelnty
- many to many relationships
- documents would become too large
- for shared entities

Use cases
- customers
- products

### Emdebbed documents
Related data in a single document structure
- Documents can have subdocuments
- Applications may need to issue less queries
- Denormalized data models
- Allow to manipulate related data in a single database operation
Provides:
- Better performance for read operations
- Ability to retrieve/update related data in a single database operation
Disadvantages:
- Documents may significantly grow
- Only one “view” of the data
Use when
- data naturally hierarchial
- data ussulaly read toghet
- updates are rare
Use cases:
- orders with items
- blog posts with commnets
- user profile wiht adresses


### Embedding vs. Referencing Trade-off
| Feature | Embedding | Referencing |
| :--- | :--- | :--- |
| **Idea** | Related data stored inside one document. | Related data stored in separate documents. |
| **Read Performance** | Fast reads (single query). | May require multiple queries or joins. |
| **Data Redundancy** | Duplication of data. | Normalized data (no duplication). |
| **Updates** | Updating duplicated data may be expensive. | Update efficiently in one place. |
| **Typical Usage** | Aggregate objects. | Shared entities. |
| **When to use:** | Data is naturally hierarchical, read together, and updates are rare (e.g., orders with items, blog posts with comments). | Data changes frequently, many-to-many relationships, documents would become too large (e.g., customers, products). |

### Data Modifications
MongoDB operations modify whole
documents or their fields
- Create - insert new document
- Read - retrieve documents using queries
- Update - modify fields in existing documents
- Delete - remove documents
```
db.orders.insertOne({...})
db.orders.find({...})
db.orders.updateOne({...})
db.orders.deleteOne({...})
```

### Insert
insertOne() → one network request per document
```
db.inventory. insertOne({
    type: "misc",
    item: "card",
    qty: 15
})
```
insertMany() → batch insert (more efficient)
```
db.inventory. insertMany([
{ type: "food", item: "apple", qty: 50, price: 0.5 },
{ type: "food", item: "banana", qty: 80, price: 0.3 },
{ type: "book", item: "notebook", qty: 40, price: 5.0
},
{ type: "misc", item: "pen", qty: 100, price: 1.2 }
])
```

### Update

```
db.inventory. updateOne(
    { item: "card" },
    { $set: { qty: 20 } }
)
```

### Aggregation pipeline
Aggregation framework processes documents in
multiple stages
- Pipeline = sequence of transformations
- Similar to SELECT → WHERE → GROUP BY → ORDER BY
- Each stage transforms the data and passes it to the
next stage

```
db.orders.aggregate([
    { $unwind: "$items" },
    {
        $group: {
        _id: "$items.product_id",
        total_qty: { $sum: "$items.quantity" }
        }
    },
    { $sort: { total_qty: -1 } }
])
```

Stages
- match
- project
- group
- sort
- limit
- unwind

### Find
Retrieves documents using simple queries.

aggratation
- tranfrom and analyzing data, multistage processing



### Indices
* Without indexes, MongoDB scans all documents (**COLLSCAN**).
* With an index, MongoDB searches using a B-tree-like index structure (**IXSCAN**).
* **Purpose:** Speed up common queries and optimize specific operations.
* **Types:** Default (`_id`), single field, compound, multikey (for arrays).

### MongoEngine
* An Object-Document Mapper (ODM) for Python.
* Maps collections and embedded documents to Python classes.
* Improves readability of application code while using standard MongoDB logic underneath.

## Replication
* Uses a Master/Slave (Replica Set) architecture for high availability.
* **Primary (Master):** Receives all write operations.
* **Secondaries (Slaves):** Apply operations from the primary to maintain an identical data set.

## Sharding
* Supported through sharded clusters for horizontal scaling.
* **Shards:** Store the actual data.
* **Query Routers (mongos):** Interface with client applications.
* **Config Servers:** Store the cluster's metadata (recommended to have 3).

## Data Partitioning (Sharding Strategies)
* **Range-based partitioning:** Shard key values are divided into non-overlapping chunks. 
    * *Pros/Cons:* Highly efficient for range queries, but can result in an uneven distribution of data (hotspots).
* **Hash-based partitioning:** Computes a hash of the shard key's value. 
    * *Pros/Cons:* Ensures a random, even distribution of data, but range queries are inefficient because they must target most/all shards.

## Transactions
- Write operations are atomic at the level of a single document
- Including nested documents (sufficient for many cases, but not all)
- When a single write operation modifies multiple documents, it is not atomic
- Other operations may interleave
- Isolation of a single write operation that affects multiple documents

| [Previous chapter](./03KeyValue.md) | [Overview](README.md) | [Next chapter](./05widecolumn.md) |
| - | - | - |
