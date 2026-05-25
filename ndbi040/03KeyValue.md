| [Previous chapter](./03NoSQLIntro.md) | [Overview](README.md) | [Next chapter](./04document.md) |
| - | - | - |


# Key-Value Stores
The simplest type of NoSQL data store, conceptually similar to a dictionary or a hash table.
* **Structure:** Like a relational table with exactly two columns:
  * **ID (Key):** Typically a string or numeric identifier.
  * **VALUE:** A BLOB (Binary Large Object) that the database just stores without necessarily understanding its contents (e.g., text, JSON, binary data, images, session state).
* **Basic Operations:**
  * `Get(key)`: Retrieve the value for the key.
  * `Put(key, value)`: Create or update a value for a key.
  * `Delete(key)`: Remove a key from the data store.
* **Pros & Cons:**
  * *Simple =* Great performance and easily scaled horizontally.
  * *Simple =* Not suitable for complex queries or data aggregation needs.

## Examples
- Riak
- Redis
- RocksDB
- memchached


## Use Cases
* **Caching:** Result cache, page cache, object cache.
* **Session Management:** Web sessions, authentication state.
* **User Preferences / Profiles:** Simple per-user settings.
* **Shopping Carts:** Where the key is the user ID or cart ID.
* **Metadata / Lookup Tables:** Fast access by a known identifier.
* **Temporary State:** Ephemeral application data.

---


# Riak
A highly distributed key-value store designed for massive scalability, fault tolerance, and high availability.
* Suitable for workloads with simple access by key.
* Includes built-in MapReduce support.
* Extends the basic key-value model with: Replication, Partitioning, Quorum-based reads/writes, and Conflict resolution.

## Data Model & Hierarchy
* **Bucket (Table):** A namespace that groups related keys. Buckets can define shared properties (e.g., replication factors or conflict-handling settings).
* **Key (Row ID):** Identifies one specific object within the bucket.
* **Value (Row):** Stores the actual data (text, JSON, binary).

## HTTP API
Riak provides a RESTful HTTP API. Objects are addressed by a combination of their `bucket` + `key`.
* **GET:** Read an object.
* **PUT:** Create or replace an object.
* **DELETE:** Remove an object.

## Advanced Features
* **Links:** Riak can store links between objects (identified by bucket + key) to express simple relationships (e.g., user → shopping cart). *Note: Links are useful for navigation but are NOT a replacement for relational joins.*
* **Riak Search:** Adds search functionality over indexed content, allowing you to query by fields inside stored values (not just by key).
  * Based on Apache Solr integration (distributed full-text engine).
  * Requires data to be indexed first.
  * Supports various MIME types (JSON, XML, plain text).


### Internals

### Consistent Hashing
* Minimizes the massive reshuffling of keys when the cluster is rebalanced (i.e., when servers are added or removed).
* The hash function maps both the physical nodes and the data keys to the same logical circle.

### The Riak Ring
* **The Ring:** The center of any Riak cluster is a 160-bit integer space forming a logical circle, which is divided into equally-sized partitions.
* **Virtual Nodes (vnodes):** Physical servers run multiple virtual nodes. Each vnode is responsible for storing a separate, specific portion of the keys on the ring. This ensures an even distribution of data, even if physical servers have different hardware capacities.

### Replication
* Each object is automatically stored on **N** separate nodes (Replication Factor, typically N = 3).
* Replicas are placed on *consecutive* partitions moving clockwise around the ring.
* **Benefits:** Provides high fault tolerance and availability. If one node fails, the data is still safe and accessible on the next nodes.

### Hinted Handoff
* **Core Philosophy:** "Store now, move later."
* Used to maintain high availability when a target replica node is temporarily unavailable (e.g., network failure, reboot).
* If the primary target is down, Riak stores the replica on another reachable node instead of failing the write.
* The temporary node keeps a **"hint"** indicating which node actually owns the data.
* Once the original target node comes back online, the temporary node automatically hands the replica over to its rightful owner.


| [Previous chapter](./03NoSQLIntro.md) | [Overview](README.md) | [Next chapter](./04document.md) |
| - | - | - |
