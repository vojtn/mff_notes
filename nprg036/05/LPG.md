# Graph use case
- connected entities -> more important that the entities themselves (if sql query with multiple 5+ joins)
- social networks
- network switched
- management hierarchies
- family trees
- discovering many different paths
    1. public transport
    2. good delivery
    3. redundancy detection


# LPG (Label Property Graph)
"Whiteboard model is the physical model"

## (Neo4j) Labeled Property Graph  Data model
1. Oriented multigraph
2. Nodes have sets of labels
3. Edges have labels
4. Nodes and Edges have sets of key-value properties


# Cypher
Query language for the labeled property graph data model
- openCypher Implementers Group
- CRUD operations
- Cypher initially developed by Neo4j - one of the graph databases
- Opened via the openCypher project
- Oracle, Tableau, Databricks (Apache Spark), SAP HANA
- their features are basis for GQL - graph query language ISO standard.


## Create

```
CREATE (:Person {name: 'James'})-[:FOLLOWS]->(:Person {name: 'John'})

```

## ASCII art
Nodes
() (p)

Labels start with : and represent types
(p:Person:Mammal)

Nodes can have properties
(p:Person {name:'John'})

Relationships
--> -[f:FOLLOWS]->

Direction of relationship can go both ways
(p1)-[:FOLLOWS]->(p2) or (p1)<-[:FOLLOWS]-(p2)

Relationships can have properties too
-[:OWNS {since: '2021-02-21'}]->


## Simple query

```
//Who uses a camera owned by a followed person?
MATCH
  (p1:Person)-[:USES]->(c:Camera)<-[:OWNS]-(p2:Person)<-[:FOLLOWS]-(p1:Person)
RETURN
  p1

```


## SET clause
SET clause allows us to add properties to variables before we return them - this change is done in the database

```
//Find James’s camera
MATCH
  (c:Camera)<-[:OWNS]-(p:Person)
WHERE
  p.name = 'James'
SET
  c.condition = 'used'
RETURN
  c

```

## Uniqueness
Constraints can be added to ensure uniqueness

```
CREATE CONSTRAINT FOR (p:Person)
REQUIRE p.name IS UNIQUE

```

## MERGE
Find or create

Tries to find p:Person named James. If such p does not exist, it creates it.

```
MERGE (p:Person {name: 'James'})
CREATE (p)-[:OWNS]->(:Laptop {vendor: 'Dell'})
```
+ON CREATE

```
MERGE (p:Person {name: 'James'})
  ON CREATE SET
    p.twitter = '@james'
MERGE (p)-[:OWNS]->(:Laptop {vendor: 'Dell'})
```


## Shortest path

```
MATCH (KevinB:Person {name: 'Kevin Bacon'} ),
      (Al:Person {name: 'Al Pacino'}),
      p = shortestPath((KevinB)-[:ACTED_IN*]-(Al))
RETURN p
```

## Relationship direction
query disregarding relationship direction
The relationship is matched even though its direction is opposite.
However, the returned relationship (w) has the original direction.


```
MATCH
 (p1:Person {name: 'John'})-[w:WORKS_WITH]-(p2:Person)
RETURN
 *
```

## Style guide

Node labels
- Case sensitive
- UpperCamelCase
i.e. beginning with an upper-case character
- :VehicleOwner rather than :vehicle_owner etc.

Relationship types
- Case sensitive
- SCREAMING_SNAKE_CASE, i.e. upper-case, using underscore to separate words
- :OWNS_VEHICLE rather than :ownsVehicle etc.

Property keys
- Case sensitive
- lowerCamelCase
- twitterHandle rather than TwitterHandle
Cypher keywords
- Case insensitive
- However, recommended to use upper-case
- MATCH rather than MaTcH


## Aggregates
Results grouped by non-aggregate fields in the RETURN statement implicitly.
No need for GROUP BY

```
MATCH (p:Person)-[:ACTED_IN]->(m:Movie)
RETURN p.name, count(*) AS numberOfMovies
```

## Filtering
```
MATCH (p:Person)-[:ACTED_IN]->(m:Movie)
WHERE m.released >= 2000
RETURN m.title, m.released, p.name
```

## WITH clause
manipulates the output before it is passed on to the following query parts

```
MATCH (n:Person)
WITH n
ORDER BY n.name DESC
LIMIT 3
RETURN collect(n.name)
```

collect -turns multiple results into a single list
(one of many available functions)

# GQL (Graph Query Language)
April 2024
Built on openCypher, PGQL, GSQL, and G-CORE languages
as of 11/2025 - not yet implemented sufficiently


# RDF vs LPG

| RDF | LPG |
| - | - |
|Made for the Web, distributed data | Made for centralized graph data |
| global identification: IRIs for everything | local node labels and edge types |
| globally reused RDF vocabularies | every database instance uses different relationship types and node labels | 
| focused on linking data from various publishers | focused on linking data from various publishers |  


RDF statement itself does not have an identifier - we cannot say anything about it.
-> Reification

## RDF-star
part of RDF 1.2 draft
Allows RDF statements to appear as subjects and objects of other RDF statements.
The triple in the subject or object position is enclosed in << >> , called “quoted triple”.
Quoted triples not necessarily asserted triples, i.e. triples forming the RDF graph.
Annotation syntax for both asserted and quoted triples.


```
#Bob states: there is someone named Alice
#There is someone named Alice, stated Bob.
<< _:a :name "Alice" >> :statedBy :bob.

#Employee22 claims that employee38's job title is Assistant designer
:employee38 :familyName "Smith" .
:employee22 :claims 
<< :employee38 :jobTitle "Assistant Designer" >> .

#Annotation syntax
:employee38 :jobTitle "Assistant Designer" 
                {| :claimedBy :employee22 |} .
```
 