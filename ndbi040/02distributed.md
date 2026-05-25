| [Previous chapter](./01motivation.md) | [Overview](README.md) | [Next chapter](./03inmemory.md) |
| - | - | - |


# Distributed Storage and Data Processing

## Distributed Storage
* Data volumes exceed the capacity of a single machine
* Need for scalability and fault tolerance
* Data is generated continuously (logs, sensors, web, media)
* Processing must run close to the data
* **Key idea:** Data is stored across many machines and accessed as a single logical system
* **Design principles:**
    * Horizontal scaling
    * Failure is normal -> replication and redundancy
    * Parallel access from many nodes

### Apache Hadoop
* Open-source framework for distributed storage and processing of large data
* Designed to run on clusters of commodity hardware
* Inspired by Google File System and MapReduce
* **Core idea:** Store and process large datasets across many machines as one system

#### Components
* **HDFS:** Distributed storage layer
* **YARN:** Resource management and scheduling
* **MapReduce:** Distributed batch processing engine
* **Hadoop Common:** Shared libraries and utilities

### HDFS (Hadoop Distributed File System)
Behaves like a standard file system (Same interface as a file system, but a different internal implementation)

#### Architecture
* **Master-slave model:**
    * **NameNode (Master):** Metadata management (stores metadata in memory)
    * **DataNodes (Workers):** Store actual data blocks (storage role)
* **Data Model:**
    * Files split into large blocks
    * Blocks distributed across cluster nodes
    * Each block is usually replicated 3 times
* **Fault tolerance:**
    * Failure is the norm, not the exception
    * Automatic re-replication

## Processing Distributed Data

### MapReduce
A programming model and execution framework designed for processing web-scale data (Origin: Google, 2004).
* **Core principle:** Divide and conquer
    * Split data into parts
    * Process parts in parallel
    * Combine partial results
* **Framework handles:** Data distribution, parallel execution, and fault tolerance
* **Programmer defines:** Only the computation logic

#### Execution Phases
* **Map:**
    * Processes input data
    * Produces intermediate key-value pairs
    * Runs in parallel on many nodes
* **Reduce:**
    * Receives all values with the same key
    * Aggregates or combines them
    * Produces the final result

#### Why it was revolutionary:
* Simple programming model
* Automatic parallelization
* Built-in fault tolerance

#### Criticisms of MapReduce:
* Step backward from declarative query languages (SQL)
* Lacks schema and data independence
* Uses brute-force scans instead of indexes
* Missing DBMS features (indexes, transactions, query optimizations)
* **Key message:** MapReduce is powerful for large-scale batch processing, but not a replacement for database systems

#### Hadoop MapReduce (Implementation)
* Open-source implementation within the Hadoop ecosystem
* Distributed batch processing engine that runs on top of HDFS
* **Characteristics:** Processes large datasets, uses disk-based intermediate storage, designed for high-throughput batch jobs
* **JobTracker (Master node):** Schedules jobs and tasks, monitors execution
* **TaskTracker (Worker nodes):** Execute map and reduce tasks, report status to JobTracker

### Apache Spark
* Next-generation unified analytics engine for large-scale data processing
* Solves MapReduce bottlenecks via **in-memory computing** (keeps intermediate data in RAM)
* Faster than MapReduce
* **Core Abstraction:** DataFrame
Provides:
- batch processing
- sql analytics
- Machine Learning
- Graph processing
- Stream processing

#### Spark application
**Driver Program**
- Runs user’s main function
- Creates SparkSession / SparkContext
- Builds execution plan
- Sends tasks to cluster
**Executors**
- Run tasks in parallel
- Store data in memory or disk
- Return results to driver
**Cluster Manager**
- Allocates resources
- Launches executors

**Spark Session**
- entry point to Spark functionality
- Creates connection to cluster and initializes execution environment

#### RDD (Resilient Distributed Dataset)
- basic distributed data structure in Spark
    - collection of elements partitioned across cluster
    - processed in parallel
- immutable
- fault-tolerant
- can be cached

#### DataFrame
Distributed table with schema
- similar to ralational table or pandas DataFrame
Features:
- structured data
- optimalized execution
- sql support
-> main abstraction in modern Spark

##### Operations
**Transformation**
- creates a new dataset from an existing one - lazily
- build execution plan
- do NOT run immediately

```
df.select("name")
df.filter(df.age > 18)
df.groupBy("age").count()
```

**Action**
- trigger execution and return results
- execute the computation
- return result to driver

```
df.show()
df.count()
df.collect()
```

##### File formats for analytics
Key idea: Format affects performance

**csv**
- row based
- human readable
- slow for analytics

**Parquet**
- columnar
- compressed
- efficient for aggregation


##### Partitioning by Column
Large datasets are often stored in separate folders/prefixes, according to selected attribute values
Example:
- e.g., region=EU/, region=US/, region=APAC/
why?
- Queries often filter by region or date
- Spark can read only relevant parts
- Less data scanned = faster analytics
-> Trade-off: too many partitions may create too many small files

##### Usage
Two ways to work with structured data in Spark
■ Both approaches produce the same execution plan

**SQL:**
- familiar relational queries
- joins, aggregations
- analysts & DB mindset

```sql
spark.sql(
    "SELECT name, age "
    "FROM people "
    "WHERE age > 18"
).show()
```

**DataFrame API:**
- programmatic pipelines
- integration with Python
- complex transformations
```
df.filter(df.age > 18) \
    .select("name", "age") \
    .show()
```

---

## Object Storage
Needs to scale storage and share by clusters -> from traditonal HDFS to modern solution **Object storage**:
* Shared persistent storage accessed via a network API
* Independent scaling 
* Access via network API
* cloud-native architecture
Used by: Spark, analytics systems, machine learning, …

### Amazon S3 Model
* Scalable distributed storage layer (Cloud service)
* **Not a database:** No SQL, indexes, transactions, or constraints
* **Data model:**
    * **Bucket:** Container/namespace
    * **Object:** Key (path inside a bucket) + data (bytes) + metadata (attributes)
    * **Logical prefixes:** Act like folders, but the storage is actually flat
* **API operations:** PUT, GET, LIST, DELETE

### MinIO (Object Storage)
High-performance object storage compatible with the Amazon S3 API.
* Stores data as objects in buckets
* Accessible over the network via HTTP API
* Can run locally or in the cloud

#### Why we use it:
* Fully S3-compatible
* Lightweight and easy to run
* Suitable for experiments and development
* Uses the exact same API as real cloud object storage
* **Operations:** PUT, GET, LIST, DELETE


| [Previous chapter](./01motivation.md) | [Overview](README.md) | [Next chapter](./03inmemory.md) |
| - | - | - |