| [Previous chapter](./04document.md) | [Overview](README.md) | [Next chapter](./06graph.md) |
| - | - | - |


# Wide-column Stores
Also known as column-family or columnar stores.
* Store data in rows with flexible columns.
* Data is organized into column families.
* Each row may contain a different set of columns, making it highly suitable for sparse and large-scale data.
* **Schema flexibility:** Columns may differ between rows.
* **Basic operations:** Insert/delete a row, retrieve rows by key, update column values.
* **Efficiency:** Fast writes and lookups by primary key; complex joins are not typical.
* **Examples:** Apache Cassandra, Apache HBase, Google BigTable.

## Use cases
* **Event logging and telemetry:** High write throughput, append-heavy data.
* **User profiles and activity data:** Rows may have different sets of attributes.
* **Content platforms:** Denormalized data grouped strictly by access patterns.

---

# Cassandra
A distributed wide-column data store originally developed at Facebook (Initial release: 2008, Apache License, written in Java).
* **Architecture:** Peer-to-peer (no master node).
* **Design Goal:** Massive scalability and high availability.
* **Operations:** Uses CQL (Cassandra Query Language) and integrates well with the Hadoop ecosystem.

## Core Terminology
* **Column:** The smallest data unit. A name–value pair with timestamp metadata (used for versioning/conflict resolution).
* **Row:** A collection of columns identified by a row key.
* **Column Family (Table):** A collection of similar rows.
* **Keyspace:** The top-level namespace that defines how data is replicated across the cluster.


## Column-Families vs. Relational Tables
* **Flexible schema:** Columns do not have to be defined in advance; schema can evolve over time.
* **Access-pattern-oriented design:** Data is grouped by how it will be queried. Denormalization is common.
* **Limited relational features:** No formal foreign keys, and joins are usually not supported at query time (secondary indexes and precomputed views are used instead).
* **Static vs. Dynamic:** * *Static:* Similar to a relational table; rows usually share the same columns.
  * *Dynamic:* Application-defined column names; highly flexible row structures.

## Special Column Types & Features
* **TTL (Time To Live):** A column value may expire automatically after a specified time (useful for sessions, logs, caches).
* **Counter columns:** Support incremental updates (useful for page views or event tracking).
* **Super Columns (Legacy):** Grouped multiple columns under one name for nested data. Rarely used today; replaced by Collections or UDTs.
* **Collections:** Supports Sets, Lists, and Maps.

## CQL (Cassandra Query Language)
SQL-like syntax
- CREATE, ALTER, INSERT, UPDATE, DELETE, DROP, TRUNCATE
- Table-oriented data model
- Since CQL 3, schema is expressed as tables (not column families)
- Simpler query model than SQL
- no joins
- limited subqueries
- queries are driven mainly by the primary key and table design

### User Defined Types (UDT)
Structured nested data inside a single column
- Alternative to joins / normalization
- Typical in denormalized read mode
- Frozen types
- Cassandra by default allows partial updates
- frozen - one atomic blob
- Entire value is read/written at once
- Cannot update individual fields inside


```
CREATE TYPE offer_udt (
    region text,
    price decimal,
    currency text,
    valid_from timestamp,
    valid_to timestamp
);
CREATE TABLE title_page_by_id (
    title_id text PRIMARY KEY,
    name text,
    offers list<frozen<offer_udt>>
);
```

## Keyspace
the top-level namespace in Cassandra
- It defines how data are replicated across the cluster

## Table
defined by columns and primary key
- partition key
- clustering column

## Column Expiration
Cassandra can automatically expire data after a specified time
- TTL is useful for sessions, logs, caches, or temporary record

## Collections
- set
- list
- map

## Querying
Cassandra supports simple queries.
Queries are most efficient when they follow the primary key
- WHERE conditions are limited compared to SQL
- ORDER BY is only supported within the clustering-key order

## cqlengine
Python object mapper for Apache Cassandra
- Cassandra tables → Python classes
- Enbes to query data using model objects
- Instead of raw CQL
- Improves readability of application code
 

## Internals

### Architecture
* **Peer-to-peer:** All nodes are equal.
* **Coordinator:** The node that happens to receive and manage a specific client operation.
* **Partitioner:** Determines how to distribute data across the nodes using a hash function.
* **Virtual nodes (vnodes):** Assign data ownership to physical nodes, making rebalancing easier.
* **Gossip Protocol:** Runs every second. Nodes exchange state messages with up to 3 other nodes to detect failures and share cluster topologies. Information has a version, so older info is overwritten by the most current state.

### Partitioning & Tokens
* The partition key is transformed into a **token** (a numeric value) by the partitioner.
* Tokens determine positions on a logical ring.
* Each node is responsible for a specific range of tokens.

### Replication
Cassandra stores each partition on multiple nodes
- Determined by the replication factor
- All replicas are equally important
- Replica placement strategies
- Tokens form a logical circular space
- Each node owns one or more token ranges
- Replicas can be placed on subsequent nodes in the ring
- This supports scalability and fault tolerance

#### SimpleStrategy
Used for a single data center. Places the first replica on a node determined by the partitioner, then places additional replicas on the next adjacent nodes clockwise around the ring.

#### NetworkTopologyStrategy
Used for multiple data centers or racks.
* Sets the number of replicas per data center.
* The first replica is placed by the partitioner.
* Additional replicas are placed by walking the ring clockwise until a node in a *different rack* is found (because nodes in the same rack often fail together).
* If no such node exists, it will fall back to a different node in the same rack.


### Gossip process
- Runs every second
- Exchanges state messages with up to 3 other nodes in the cluster
- Enables to detect failures
- Gossiped message:
- Information about a gossiping node + other nodes that it knows about
- Acquired:
- Directly = by direct communication
- Indirectly = second hand, third hand, …
- Has a version
- Older information is overwritten with the most current stat

| [Previous chapter](./04document.md) | [Overview](README.md) | [Next chapter](./06graph.md) |
| - | - | - |
