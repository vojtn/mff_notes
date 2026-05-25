| [Previous chapter](./08multimodel.md) | [Overview](README.md) | [Next chapter](./10evolution.md) |
| - | - | - |


# Specialized and Emerging Database Systems
Not all data problems are best solved by classical relational DBMS. 
Modern workloads require specialized systems:
* Similarity search over embeddings → Vector DBMS
* Multidimensional scientific arrays → Array DBMS
* Geospatial indexing / geometry → Spatial DBMS
* Globally distributed ACID SQL at scale → NewSQL
* Uncertain / incomplete data reasoning → Probabilistic DBMS

→ rise of specialized database systems

## Array databases
Stores data as multidimensional arrays rather than flat tables.
* **Core idea:** Consists of dimensions (coordinate axes), cells (positions), and attributes (values in cells).
* **Why use it?** Some data is naturally multidimensional (biology, physics, astronomy, climate).
* **Natural dimensions:** Space (x, y, z), time, wavelength, experiment/sample.
* **Relational problem:** Tabular storage is possible but unnatural; creates too many tuples for dense grids.
* **Dense Arrays:** Most cells contain values (e.g., image pixels, matrices).
* **Sparse Arrays:** Many cells are empty (e.g., graphs, sensor gaps).
* **Example System:** SciDB (designed for complex analytics on massive multidimensional arrays).

### Chunk-Based Storage and Distribution
Large arrays are partitioned into chunks (the basic unit of storage, transfer, and parallel processing).
* **Chunk Size (I/O vs. Parallelism):** * Larger chunks = fewer metadata entries, better sequential reads, efficient full scans.
    * Smaller chunks = more parallel tasks, better selective access, finer load balancing.
* **Chunk Shape:** Chosen based on workload locality and query patterns (e.g., row scans vs. window queries).
* **Placement Policy:** * Hash-based: Good balance, random placement, weak locality.
    * Range-based: Preserves order/locality, good for range scans, risk of hotspots.
    * Cost-aware: Uses workload statistics, hard to maintain.
* **Replication:** Benefits (fault tolerance, faster local reads) vs. Costs (extra storage, update coordination).

## New SQL
"Keep SQL, rebuild the engine."
Distributed relational database systems designed for scale-out OLTP.
* **The Problem:** Scaling traditional SQL is hard (vertical limits, complex sharding, difficult failovers).
* **The Solution:** SQL + ACID + Horizontal scalability.
* **Properties:** SQL interface, relational model, ACID transactions, automatic partitioning/sharding, replication, fault tolerance.
* **Goal:** Preserve DBMS functionality while supporting high throughput and distributed operation.

### Examples
- TiDB
- Volt Active Data
- yugabyteDB
- CockroachDB


## Vector Databases
Designed for modern AI systems that use embeddings instead of exact keys.
* **Core task:** Similarity search in high-dimensional space.
- text embeddings
- image embeddings
- audio embeddings
- user / product representations
Typical queries:
- semantic search - find documents whose embeddings are nearest to the query embedding
- recommendation - find products / users / items nearest to a user or item embedding
- duplicate detection - find objects with almost identical embeddings
- clustering support - group vectors that are close to each other

-> vector databases use specialized indexing methods

### Embedding
dense numerical representation of an object in a vector space E.g. word, sentence, document, image, audio segment, user or product profile, …
The representation is learned so that semantically or structurally similar objects are mapped to
nearby vectors
* **Properties:** Fixed dimensionality, real-valued coordinates, model-dependent meaning.
* **Similarity measures:** Cosine similarity, Euclidean distance, scalar product.
* **Indexes:** Because brute-force calculation is too slow, systems use specialized indexes like HNSW (Hierarchical Navigable Small World) for fast approximation.

### Similarity in Vector Space
Vector search does not ask whether two objects are identical, it asks how close their vector representations are
Intuition:
- smaller distance → more similar objects
- smaller angle → more similar direction
- higher inner product → vectors point in more similar directions
The choice of metric matters because it affects:
- ranking of results
- index design
- query semantics
Different embedding models are often designed with specific similarity measures
in mind

### Qdrant
* Open-source vector database with REST API.
* **Data model:**
    * Collection = named set of searchable points.
    * Point = ID + vector + optional payload (metadata used for filtering).
* Each collection defines vector dimensionality and distance metric.
* Typical use cases: semantic search, recommendation, image similarity, duplicate detection, ..

## GeoSpatial Databases
Manage data with location, shape, or geometry (e.g., maps, GPS tracks).
* **Spatial data properties:** Geometry, position, shape, size, distance.
* **Spatial data types:** Point, LineString, Polygon, MultiPoint / MultiLineString / MultiPolygon.
* **Database capabilities:** Spatial predicates, nearest-neighbor search, routing, map analytics.
* **Indexing:** Uses specialized indexes like R-trees to group nearby objects via bounding boxes.

### PostGIS (Example System)
* Open-source geospatial extension for PostgreSQL.
* Adds native spatial support to a relational DBMS.
* **Core features:** Geometry/geography types, spatial predicates (intersects, contains, within, touches).

| [Previous chapter](./08multimodel.md) | [Overview](README.md) | [Next chapter](./10evolution.md) |
| - | - | - |

