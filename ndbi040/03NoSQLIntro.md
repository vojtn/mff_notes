| [Previous chapter](./03inmemory.md) | [Overview](README.md) | [Next chapter](./03KeyValue.md) |
| - | - | - |

# Introduction to NoSQL data Stores
Traditional relational databases are not always the best fit for modern applications.
Modern apps require:
* Massive volumes of data
* Distributed systems
* Real-time processing
* Flexible schemas

## SQL vs. NoSQL
* **Traditional (SQL) databases:** Relational model, fixed schema, ACID transactions, strong consistency.
* **NoSQL databases:** Flexible data models, horizontal scalability, distributed architectures, often relaxed consistency.

## NoSQL motivation
* **Web-scale systems:** Required to handle large datasets, distributed architectures, and performance/scalability.
* **Pioneers:** Huge companies like Google, Amazon, and Facebook needed databases that could scale horizontally across thousands of commodity machines.

## Data Model (Aggregate Orientation)
* Data that is accessed together is stored together.
* **One aggregate = one unit of storage.**
* No joins are required to reconstruct objects.

---

# Core Distributed Concepts

## BASE Properties
The NoSQL alternative to ACID transactions.
* **Basically Available:** The system works basically all the time; partial failures can occur but don't take down the whole system.
* **Soft State:** The state of the system is in flux and non-deterministic (it may change without input due to replication).
* **Eventual Consistency:** The system will eventually be in some consistent state at some time in the future once data propagates.

## CAP Theorem (Brewer’s Theorem)
In a distributed system, it is impossible to guarantee all three of the following properties simultaneously (you must choose two, usually CP or AP because P is unavoidable):
* **Consistency (C):** All nodes see the same data at the same time.
* **Availability (A):** Every request receives a non-error response.
* **Partition Tolerance (P):** The system continues working despite network failures or dropped messages.

--- 

## Sharding (Data Partitioning)
Splitting data across multiple machines.
* **Benefits:** Horizontal scalability, increased storage capacity, parallel query processing.
* **Challenges:** Choosing a data distribution strategy, handling cross-shard queries, rebalancing when nodes are added or removed.
* **Common techniques:** Range partitioning, Hash partitioning.

## Replication
Storing multiple copies of the same data across different nodes.
* **Benefits:** Fault tolerance, high availability, faster reads.
* **Challenges:** Keeping replicas consistent, conflict resolution, replication lag.
* **Replication factor (N):** The number of copies (Common default: N = 3).

### Replication Architectures
* **Master-Slave:**
    * *How it works:* One node acts as the master (accepts all writes and propagates changes). Replicas (slaves) receive updates and often serve read requests.
    * *Advantages:* Simple design, easy consistency control.
    * *Limitations:* Master is a potential bottleneck; master failure requires a failover process.
* **Peer-to-Peer:**
    * *How it works:* All nodes are equal. Any node can accept reads and writes, and data is replicated across nodes (no single master).
    * *Characteristics:* No single point of failure, high availability, requires distributed coordination.
    * *Challenges:* Conflict resolution, eventual consistency, more complex protocols.

---

# Types of NoSQL databases
- Key-value: Redis, riak
- doument - mnogoDB
- column Store: cassandra
- graph: neo4j
These systems differ mainly in how data
is modeled and accessed

## Key-value stores
The simplest NoSQL data stores (conceptually similar to a hash table).
* **Model:** Like a table with two columns (ID and VALUE). The value is often a BLOB (Binary Large Object) that the database doesn't interpret.
* **Basic operations:** `Get` value by key, `Put` value for a key, `Delete` key.
* **Pros:** Unmatched performance, easily scaled.
* **Cons:** Not suitable for complex queries or aggregation needs.
* **Examples:** Redis, Riak.

## Column-family stores
Data is organized into rows and column families (Inspired by Google BigTable).
* **Model:** A row key identifies a record. Columns are grouped into column families.
* **Features:** Columns within a row can differ; new columns can be added dynamically. Data is often stored with timestamps for versioning.
* **Basic operations:** Read a row by key, insert/update columns, delete columns or rows.
* **Examples:** Apache Cassandra, HBase.

## Document systems
tore data as self-describing hierarchical structures (JSON, BSON, XML).
* **Model:** Documents are grouped into collections. They are a natural representation of application objects.
* **Features:** Flexible schema (fields may differ between documents). Offers rich query capabilities, though complex joins are not typical.
* **Basic operations:** Insert/delete a document, retrieve documents by query, update document fields.
* **Examples:** MongoDB, CouchDB.

## Graph Systems
Designed to store entities and their relationships.
* **Model:** Data represented as Nodes (entities), Edges (relationships), and Properties (attributes).
* **Features:** Optimized for graph traversal (finding neighbors, searching paths). Efficient for highly connected data.
* **Challenges:** Distributing (sharding) large graphs across multiple servers is notoriously difficult.
* **Examples:** Neo4j.

---

# Schemaless Data Model
Many NoSQL databases support flexible or dynamic schemas where records in the same collection do not have to share an identical structure.
* **Advantages:** Flexible data model, easier evolution of applications, suitable for rapidly changing data.
* **Challenges:** Weaker database-level data validation, the application code must handle the data structure, harder to enforce overall consistency.

# Polyglot persistence
"Use the right tool for the job." Modern applications often use multiple database technologies because different systems are optimized for different workloads.
* **Relational databases:** Transactions, highly structured data.
* **Key-value stores:** Caching, fast lookups, sessions.
* **Document databases:** Flexible data structures, CMS, catalogs.
* **Graph databases:** Relationship-heavy data, recommendations, fraud detection.


| [Previous chapter](./03inmemory.md) | [Overview](README.md) | [Next chapter](./03KeyValue.md) |
| - | - | - |