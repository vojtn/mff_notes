| [Previous chapter](./05widecolumn.md) | [Overview](README.md) | [Next chapter](./07searchIR.md) |
| - | - | - |


# Graph Data Management
Property graph databases, graph store. 
- Data are stored as nodes and relationships
- often flexible schema       

typical operations:
- find a node or neighborhood
- traverse relationship
- good for highly interconnected data  
Joins are replaced by traversals


## Property Graph Model
two types
- Labeled Propery Graph (LPG) - schema-later (Neo4j)
- Typed Propery Graph (TPG) - schema-first

Node
- identifier
- labels
- properties

Relationship
- directed edge between two nodes
- type
- properties

Property
- key-value pair

```
(Alice:Person {age: 30})-[:KNOWS {since: 2022}]->(Bob:Person)
(Alice)-[:LIVES_IN]->(Prague:City)
```


## Neo4j
One of the best-known property graph databases
- open source, Java, Cross-Platform
- 2007
- Data: Nodes, relationships, labels and properties
- Data model: labeled property graph

labels/types
Nodes - 0.n labels
Relationships !1 type

### Cypher 
Query language
- declarative
- inspired by SQL and SPARQL
- based on graph patterns

#### Match
find a pattern
```
MATCH (a:Person {name: 'Alice'})
```

#### Create
create nodes/relationships
```
CREATE (a:Person {name: 'Alice', age: 30})
-[:LIVES_IN]->
(:City {name: 'Prague'})
```

#### Set
Updates properties/lables
```
MATCH (a:Person {name: 'Alice'})
SET a.age = 31
RETURN a
```

#### Where
Add condition
```
MATCH (a:Person)-[:KNOWS]->(b:Person)
WHERE a.name = 'Alice'
RETURN b
```

#### Detach Deletee
remove data
A node with existing relationships cannot be deleted by DELETE alone

```
MATCH (b:Person {name: 'Bob'})
DETACH DELETE b
```

#### REMOVE 
removes label/property

```
MATCH (a:Person {name: 'Alice'})
REMOVE a.age
RETURN a
```

#### With
Used to pass intermediate results to the next part of a query
- It allows us to:
- Carry selected variables forward
- Rename values with AS
- Use aggregation results in later steps
```
MATCH (a:Person)-[:KNOWS]->(b:Person)
WITH b, count(*) AS popularity
WHERE popularity >= 2
MATCH (b)-[:LIVES_IN]->(c:City)
RETURN b.name AS person, popularity, c.name AS city
```

#### Match vs Optional match
- MATCH requires the pattern to exist
- OPTIONAL MATCH keeps the row even if the pattern is missing
- Similar to inner join vs. left outer join
- Missing values are returned as null

```
MATCH (a:Person {name: 'Alice'})
OPTIONAL MATCH (a)-[:LIVES_IN]->(c:City)
RETURN a.name AS person, c.name AS city
```

#### Directions in patterns
-[]-> uses the stored direction
-[]- ignores direction in the match
Useful when direction is not important for the query


### Neomodel
Low-level:
- Cypher via driver (full control)
- Explicit queries
High-level:
- OGM (Object Graph Mapping)
- Similar to ORM
- Work with Python objects instead of queries

### Path
one or more nodes connected by relationships
- Can be returned directly as a query result

### Traversal
visiting nodes by following relationships
- Follows some rules:
- relationship type
- relationship direction
- traversal order (e.g., BFS / DFS)

### Transaction management
Unit of work executed atomically

In neo4j:
- Every query runs inside a transaction
- Support for ACID properties

#### Implicit
- created automatically for a single query
- usually committed automatically if the query succeeds
Use implicit when one simple query is enough

#### Explicit
started and controlled by the application
- can contain multiple queries / updates
- committed explicitly
- rolled back if an error occurs
Use explicit when several steps must succeed together


## Indexes
- Without index: Database may need to scan many nodes
- With index: Database can find matching nodes directly

Typical use:
- find a person by name
- find all movies from a given year

Index
- Used to find entry points in the graph
- Based on property values

Traversal
- Used to explore connected data
- Follows relationship

Traversal follows relationships, but an index helps us find the starting node

```
MATCH (p:Person)
WHERE p.name = 'Alice'
RETURN p
CREATE INDEX person_name_index
FOR (p:Person)
ON (p.name)
MATCH (p:Person {name: 'Alice'})
-[:KNOWS]->(f:Person)
RETURN f.name
```

## Gremlin
traversal-based graph query language
- procedural language
- says how to do that not what
- pipeline

```
g.V().has("name","Alice")
g.V().has("name","Alice").out("KNOWS")
g.V().has("name","Alice").out("KNOWS").values("name")
g.V().has("name","Alice").out("KNOWS").count()
g.V().has("name","Alice").out("KNOWS").out("KNOWS")
g.V().hasLabel("Person").has("age", gt(30)).values("name")
```


## RDF (Resource description framework)
data as triples (subject - predicate - object)
- no explicit properties on nodes or edges

Usecases
- integration data from many sources
- standard representation
- interoperability
- semantice web
- linked open data
- more uniform and standardised

| [Previous chapter](./05widecolumn.md) | [Overview](README.md) | [Next chapter](./07searchIR.md) |
| - | - | - |
