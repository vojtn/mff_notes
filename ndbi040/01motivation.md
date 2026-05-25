| [Overview](README.md) | [Next chapter](./02distributed.md) |
| - | - |

# Big data

## Views of data

### Conceptual
- what exists in reality
- object and relationships
- ER, UML
### Logical
- How data is represented
- Relational, JSON, graph

### Physical
- how data are stored
- Files, indexes

## Relational Model
* Introduced by E.F. Codd, 1970
* Core idea: represent data as relations (tables), manipulate using declarative logic
* Concept: sets of tuples, relation definition (schema), integrity constraints, declarative queries (SQL)
* Revolutionary because:
    * Separation of logical & physical layers
    * Data independence
    * Set-based operations
    * Strong mathematical basis

### Long-Term Domination
* Simplicity
* Mature systems
* Strong theory
* Standardization (SQL ISO)
* Huge ecosystem and tooling
* Highly optimized
* Limitation: not all data is tabular (e.g., logs, documents, multimedia, connected, time-series, spatial)

## Data models evolution
Navigational (60s)
- hierarchial, network

Relational (70s)
- declarative SQL

Post-relational(90s)
- object-relational
- XML
- NoSQL, graph

Today
- polyglot
- multimodel
- cloud data platforms


## Whats Big Data?
high volume, high velocity, and/or high variety information assets that require new forms of processing to enable enhanced decision making, insight discovery and process optimization.

### Gartner
Information technology research and advisory company
- Founded in 1979 by Gideon Gartner
- USA, Stanford
Provides: competitive analysis reports, industry overviews, market trend data, product evaluation reports

### Big Data sources
- Socal media
- Mobile devices
- sensors networks
- scientific instruments

### Charactericrs

#### Volume (Scale)
Massive data volume
- terabytes → petabytes → exabytes
- continuous growth
- data stored across many machine

#### Variety (Complexity)
Data comes in many forms
- structured (tables)
- semi-structured (JSON, XML)
- unstructured (text, images,
video)
- graph & network data

#### Velocity (Speed)
Continuous data streams
- real-time user
interactions
- sensor streams
- financial transactions
- logs & monitoring data

Data must be processed in real time.

#### Veracity (Uncertainty)
Data may be:
- incomplete
- noisy
- inconsistent
- uncertain
Sources differ in reliability.
More data does not always mean better data.

## Vertical Scaling (Scaling up)

Traditional approach
- strong consistency
- centralized architecture
- Bigger machines -> more CPU, RAM, Storage

Limitations
- expensive hardware
- vendor lock-in
- physical limits of a single machine

## Horizontal Scaling (scaling out)
- distibuted system across many nodes
- commodity hardware

Limitations
- latency
- network reliability
- network security

Modern Database Systems for Big Data  
New requirements:
- distributed by design
- horizontally scalable
- fault tolerant
- flexible schemas
- high throughput   

Result - new database families:
- NoSQL databases
- Key/value, column, document
- Graph
- NewSQL databases
- Multi-model databases
- Array databases

## NoSQL
* Core motivation: solving problems where relational databases are a bad fit

### Aggregates

#### Aggregate-oriented systems
(store data together)
- data grouped into aggregates
- one aggregate = one unit of
storage
- retrieved in one read
- no joins needed
- optimized for specific queries
Examples:
document, key–value, column-family

#### Aggregate-ignorant systems
(store data separately)
- data split across tables
- relationships via references
- joins reconstruct objects
- flexible querying across data
- optimized for ad-hoc queries
Examples:
relational databases (SQL)

| [Overview](README.md) | [Next chapter](./02distributed.md) |
| - | - |
