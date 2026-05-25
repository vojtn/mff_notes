| [Previous chapter](./09special.md) | [Overview](README.md) |
| - | - |

# Evolution management in Big Data systems
*Evolution management* = controlled adaptation under constraints
long live systems -> 
- schema changes
- workload changes
- scale changes
- ownership changes

Systems are designed once, used for years
- schema
- workload
- scale
- hardware
- regulations

-> all of that change during system lifetime


## Forces that break the original design
Application driven
- new etities
- new attributes
- new relationships
- new APIs

Workload driven
- new queries
- higher concurrency
- stricter response-time requirements
- analytical workloads added

Infrastructure driven
- cloud move
- distributed deployment
- move old-data to cheaper storage

Governance driven
- keeping old data for years
- history of data changes required
- GDPR



- Small change has large impact

Dev teams are rewarded by delivering features, hit benchmarks and not future migration ease, safe rollback, etc.. -> technical debt in data layer

## Evolution in Big Data systems
Way harder due to
- many pipelines
- distributed consistency
- no downtime allowed
- multiple engines
- multiple schemas
- multiple owners

### Schema
Schema provides
- schemantics - what data means?
- integrity - what values are legal?
- optimalization - how queries can be executed efficiently?

! Schemaless is not schema-free !
Even without schmea, there is a hidden schema in the code itself

### Schema on write
- Validate before storing
- Examples: PostgreSQL, MySQL, ...
- Advantage: consistency
- Risk: less flexibility for new data

### Schema on read
- Validate during query/use
- Examples: JSON data lake, logs on S3, …
- Advantage: flexibility
- Risk: late failures

## Migration
Move production system to new stable state
- changes running infrustructure
- ussually persistant
- affects delpoyment/runtime
- system-oriented

### Concerns:
- downtime
- rollback
- consistency

### Examples
- PosgteSQL -> clound managed PostgreSQL
- MongoDb -> Cassandra read model
- single node -> distributed cluster
- on prem -> cloud

Migration is rarely 1:1 Copy, Different systems optimize different workloads
- schema redesign
- denormalization
- re-partioning
- query rewriting

## Transformation
Preserve meaning while changing structure
- changes data structure
- semantic focus
- often repeatable
- data-oriented

### Concerns
- rename field
- split field
- move
- nesting

### Examples
- JSON -> relational rows
- CSV -> Parquet

## Big data evolution is difficult
- 10 TB 
- multiple distributed replicas
- 24/7 availability
- many connected systems

### Operational Techniques for Big Data Evolution

#### Rolling deployment
System is updated gradually instead of full shutdown
- reduce downtime
- reduce risk
- verify incrementally

#### Continuous validation
Migration correctness is checked during execution
Typical checks:
- row/document counts
- missing values
- schema consistency

#### Rollback planning
- Migration may fail
- Need strategy for safe recovery
Approaches:
- snapshots
- dual-write phase
- replay from logs
- fallback to previous cluster

### Evolution Patterns
Manage transition from old system/state to new one
| Pattern | Basic Idea | Useful For | Main Risk |
| :--- | :--- | :--- | :--- |
| **Big bang** | Stop old system → migrate → start new system. | Small systems, maintenance window possible. | Downtime, hard rollback. |
| **Blue/Green** | Old and new systems run in parallel; traffic is switched later. | Safer production switch. | Data divergence. |
| **Dual Write** | Application writes temporarily to both old and new targets. | Zero-downtime transition. | Inconsistent writes. |
| **CDC sync** | Changes from old DB are captured and replayed to new system. | Large data, continuous writes. | Lag, schema compatibility. |

---

### Transformation patterns
Manage change of data shape, format, or meaning

| Pattern | Basic Idea | Example | Main Risk |
| :--- | :--- | :--- | :--- |
| **ETL** | Transform before loading to target. | Mongo JSON → Cassandra rows. | Transformation bug before load. |
| **ELT** | Load raw data first, transform inside target. | Logs → lake → warehouse tables. | Raw zone grows, late errors. |
| **Batch rewrite** | Rewrite existing historical data. | CSV → Parquet. | Expensive full scan/copy. |
| **Stream enrich** | Transform events as they arrive. | Add customer segment to order events. | Late/missing reference data. |
| **Materialized view** | Recompute derived read model. | `orders_by_city` table. | Stale or inconsistent view. |

## Tools
Manual evolution does not scale

Modern systems require coordination of:
schema versions, pipelines, replicas, streaming systems, connected analytics and services, dashboards

must provide:
- version tracking
- orchestration
- synchronization
- rollback
- observability
- validation

### Flyway
Open-source schema migration system
- Redgate
Goal: 
- Keep database schema synchronized with application evolution
Philosophy: Database schema should evolve similarly to source code -> versioned, reproducible, automated, tracked in Git
Supported databases: PostgreSQL, MySQL, MariaDB, Oracle, SQL Server, SQLite,
Cassandra, Snowflake

### Debezium
Open-source CDC platform
- Built on Kafka Connect ecosystem
- Supported databases: PostgreSQL, MySQL, MongoDB, SQL Server, Oracle,
Cassandra

### Apache NiFi
Open-source visual dataflow system
- Pipeline orchestration + transformation platform
Main goal: build and manage dataflow pipelines visually
Core philosophy: Data movement should be observable, configurable, traceable, replayable, backpressure-aware

### Core Model
Dataflow as pipeline:
source → processors → queues → target systems
* Processor - active operation

* Queue - buffer between processors

* FlowFile - single moving data object

## Apache Iceberg
Open table format for large analytical datasets
- Designed for: data lakes, lakehouses, PB-scale analytics
- Traditional approach: schema change → rewrite all data

Iceberg updates metadata instead of rewriting all historical files immediately

## Multi-Model Evolution Management

Different systems require different evolution strategies because one logical change must propagate into different storage models, query languages, and schemas.

* **Relational systems (e.g., PostgreSQL):** Evolution involves `ALTER TABLE`, modifying indexes, and changing normalization under strong schema enforcement.
* **Column-family systems (e.g., Cassandra):** Evolution involves query-oriented redesign, denormalization, and repartitioning driven by workload.
* **Document databases (e.g., MongoDB):** Evolution involves partial schema evolution, mixed document versions, and lazy migration, often leaving compatibility handling to the application.
* **Search systems (e.g., Elasticsearch):** Evolution involves reindexing, analyzer changes, and mapping evolution, often requiring complete index rebuilds.

| [Previous chapter](./09special.md) | [Overview](README.md) |
| - | - |