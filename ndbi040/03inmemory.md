| [Previous chapter](./02distributed.md) | [Overview](README.md) | [Next chapter](./03NoSQLIntro.md)  |
| - | - | - |

# In memory and Embedded Data Stores
* **In-memory** describes *where* data is stored.
* **Embedded** describes *how* the database is deployed.

## Latency Hierarchy
* L1 cache ~ 1 ns
* RAM ~ 100 ns
* SSD ~ 100 μs
* HDD ~ 10 ms
* **Key takeaway:** Accessing disk instead of memory can be 100,000× slower.

## Architectural Implications
Data placement determines system behavior:
* **Disk-based systems:** I/O-bound
* **Memory-based systems:** CPU-bound
* **Distributed systems:** Network-bound

## The Database Bottleneck
* **Typical architecture:** Clients → App → Database
* **Problems:** Many repeated reads cause the database CPU and disk I/O to become bottlenecks.
* **Solution (Memory Layer):** Clients → App → CACHE → Database
* **Benefits:** Faster reads, lower DB load, better scalability.

## Two Database Dimensions
* **Storage Model:** 
    * In-memory (RAM) - e.g., Redis
    * Disk-Based (Disk) - e.g., PostgreSQL
* **Deployment Model:** 
    * Embedded (Runs inside the app) - e.g., SQLite
    * Server-based (Separate database server) - e.g., PostgreSQL

---

# In Memory databases
Primary storage is RAM
- Extremely low latency (microseconds)
- Often used as key-value stores
- Persistence is optional/asynchronous
## Advantages
- Very fast reads and writes
- Suitable for real-time workloads
- Efficient for high-throughput systems
## Disadvantages
- RAM is expensive
- Risk of data loss without persistence
- Often limited dataset size
## Typical uses:
- caching layers
- session storage
- streaming analytics
- leaderboards / counters
## Examples
- Redis
- saphana
- memcached
- voltdb

# Embedded Databases
- DBMS is embedded in the application
- No separate server process
- Application communicates via direct library calls

## Advantages
- Zero configuration
- Very small footprint
- No network overhead
- Easy deployment
## Disadvantages
- Limited concurrency
- Usually single-node
- Not ideal for distributed systems
## Typical uses:
- mobile apps
- desktop applications
- IoT devices
- local caches
## Examples
- SQLite
- RocksDB
- LevelDB

# SQLite
Most widely deployed database
- Single-file database
- No server process
- Runs directly inside the application
    - It is accessed through a library
- Typical environments: mobile apps, web browsers, desktop applications, IoT devices

---

# Redis
Open-source database
- First release 2009, Written in C
- Clients for many languages
- Key-value store with advanced data structures
- Atomic operations, Primary in-memory dataset
- Persistence: dumping the dataset to disk periodically / appending each command to a log
Typical roles:
- caching, session storage, real-time analytics, 

## Keys and Values
* **Keys:** Binary safe (any binary sequence can be a key).
* **Values:** Can be complex objects (Strings, Hashes, Lists, Sets, Sorted Sets).
* **Capabilities:** Can perform range, diff, union, and intersection operations atomically (unusual for standard key-value stores).

## Data Types
- String
- Hash - A structured object stored under a single key
- List - Lists of strings, sorted by insertion order
- Set - Unordered collection of non-repeating strings
- Sorted Set - Non-repeating collection of strings


## Time To Live
Allows Redis keys to expire automatically
* **Important:** TTL is defined on *keys*. Expiration removes the *entire* object.

---

# Caching Concepts

## Caching vs Persistence
* **Caching:** Appropriate for temporal data to improve performance (e.g., session data, API responses, recent objects).
* **Persistence:** Appropriate for permanent source-of-truth data (e.g., orders, payments, user accounts).

## Caching patterns
Different strategies for interaction between cache and database

### 1. Cache-aside (Lazy Loading) - *Most Popular*
The application loads data into the cache only when needed.
* **Cache Hit:** App → Redis → Data
* **Cache Miss:** App → Redis (miss) → Database → Redis (store)
* **Characteristics:** Database is the source of truth, cache is populated on demand. First request is slow (miss), subsequent requests are fast (hit).
* **Typical use:** Product pages, user profiles, API responses.


### 2. Write-Through Cache
All writes go through the cache *before* reaching the database.
* **Characteristics:** Cache always contains fresh data, simpler reads. Writes are slower because they require two steps (Cache + DB).
* **Typical use:** Systems requiring strong consistency (financial or transactional systems).

### 3. Write-Back Cache (Write-Behind)
Writes go *only* to cache; the database is updated later asynchronously.
* **Characteristics:** Very fast writes, massive reduction in database load. High risk of data loss if the cache fails before syncing to the DB.
* **Typical use:** High-throughput systems, analytics pipelines, buffering writes.

## Cache Invalidation
Problem: Cache may return outdated (stale) data.
* **TTL (Time-based expiration):** Simple, but data may be stale until the timer expires.
* **Explicit invalidation:** On update, explicitly DELETE the cache key (Pattern: UPDATE database → DEL cache key). Provides stronger consistency.

## Cache Eviction (Handling a Full Cache)
When RAM is full, the system must remove items to make room.
* **LRU (Least Recently Used):** Removes the item that hasn't been accessed for the longest time.
* **LFU (Least Frequently Used):** Removes the item accessed the fewest number of times.
* **FIFO (First In, First Out):** Removes the oldest item.


| [Previous chapter](./02distributed.md) | [Overview](README.md) | [Next chapter](./03NoSQLIntro.md)  |
| - | - | - |