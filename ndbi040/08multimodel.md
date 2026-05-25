| [Previous chapter](./07searchIR.md) | [Overview](README.md) | [Next chapter](./09special.md) |
| - | - | - |


# Multi-Model Data Management and System Integration
## The Challenge: Data Variety in Big Data
Modern applications deal with high structural heterogeneity:
- tree data
- graph data
- tabular data
- temporal and spatial data
- text


## Polyglot Persistence
Use the right tool for the job
- Document store → for structured data with differences
- Graph store → for relations
- Key/value store → for simple managed structure
However the integration is hard

Pros
- handles multi-model data
- helps apps scale
- rich experience, mature systems -standards
Cons
- requires integration expertise
- developers must learn multiple DBs
- challenge of cross-model queries and transactions


## Multi-Model Databases
Designed to support multiple data models (table, XML, JSON, text, RDF) against a single, integrated backend.
* **Origin:** Evolved from object-relational database systems (ORDBMS).
* **Convergence trend:** Leading DBMSs are gradually adding support for multiple models:
    * Relational systems add JSON/XML support.
    * Document systems add joins and graph-like operations.

Pros:
- handles multi-model data
- one fault-tolerant system
- ensures data consistency
- unified query language

Cons:
- complex
- relatively immature compared to single-model systems
- lack of standards

### Classification (Based on Original Model)
* **Relational:** PostgreSQL, SQL Server, IBM DB2, Oracle DB, MySQL
* **Document:** ArangoDB, Couchbase, MarkLogic, MongoDB, Cosmos DB
* **Graph:** OrientDB
* **Key/value:** Riak, Oracle NoSQL DB
* **Column:** Cassandra, CrateDB, DynamoDB, HPE Vertica


## Multi-Model Database Challenges
* **Modeling and Representation:** Open data models, schema/model evolution, and choosing between references vs. embedding vs. redundancy.
* **Storage and Indexing:** Building multi-model index structures, handling different access patterns (Graph/JSON/Table), and dealing with the lack of a universal index.
* **Query and Processing:** Creating a unified query language, processing cross-model queries, and dealing with the lack of a universal optimizer.
* **Transactions and Consistency:** Handling multi-model transactions, choosing between ACID vs. eventual consistency, and ensuring consistency across different representations.

## ArangoDB
An open-source multi-model DBMS.
* **Document-first system:** Data is stored in collections; a document is a JSON-like object.
* **Supports:** Document model, graph model, and key/value access.
* **Graph Model:** Uses two types of collections: Vertex collections (nodes) and Edge collections (relationships with `_from` and `_to` attributes).
* **AQL (Arango Query Language):** A unified, declarative query language for all models.
* **System Attributes:** Every document has:
    * `_key` = local identifier (within a collection)
    * `_id` = global identifier (`collection/_key`)
    * `_rev` = revision (changes on update)

### AQL Arango Query Language
declarative query language
- Designed for JSON-like data
- Works over documents and graphs
Supports:
- filtering (FILTER)
- projection / return (RETURN)
- aggregation (COLLECT, AGGREGATE)
- sorting (SORT), limiting (LIMIT)
- traversals
- shortest path queries
- ...

```
FOR x IN collection
FILTER ...
SORT ...
LIMIT ...
RETURN ...
```


## Integration Strategies for Multi-Model Data
* **Multi-model databases:** One single, integrated backend.
* **Polyglot Persistence:** Multiple stores integrated by the application.
* **Polystores:** A federated query system sitting on top of multiple data storage technologies used jointly.

### Polystores Types
* **Loosely-coupled:** Mediator-wrapper style. Common interface with high autonomy for local stores.
* **Tightly-coupled:** Direct use of local interfaces. Better performance but lower autonomy.
* **Hybrid:** Combines both approaches.

### Polystored dimensions
- heterogeneity
- autonomy
- transparency
- flexibility
- optimality

### Why Integration is Hard
Integration must bridge all layers because every engine has its own:
* Model
* Query language
* Optimizer
* Consistency model

**Query Processing Pipeline in Polystores:** Parse query → split into subqueries → run in local engines → move partial data → join/merge results.


## Trino
A distributed SQL query engine for interactive analytics (originally built by Facebook).
* Queries multiple external systems through connectors.
* Data remains in the source systems; Trino federates access at query time.
* **Architecture:** Coordinator node (parses, plans, and schedules queries) + Worker nodes (execute tasks and fetch data from sources).
* Designed for federated querying across heterogeneous systems (analytics, reporting, investigation).
* It is a query layer, **not** a new source of truth.
* SQL supports filtering, joins, aggregation, and cross-catalog queries.
* **Note:** Performance still depends heavily on the source systems and their pushdown support (ability to process parts of the query locally).

| [Previous chapter](./07searchIR.md) | [Overview](README.md) | [Next chapter](./09special.md) |
| - | - | - |