# SPARQL
Query language for RDF data

## SPARQL endpoint
- HTTP-based web service
- input: SPARQL query
- output: data
    - RDF
    - CSV
    - JSON
    - XML
    - ...
- typically including a user form
or use https://yasgui.triply.cc/

### Examples:
https://github.com/OpenLinkSoftware/lod-cloud 

https://query.wikidata.org/

https://data.europa.eu/sparql

https://data.gov.cz/sparql 

## Querying

### Variable
Variables can appear at any triple (quad) position, i.e. as a subject, predicate, object, or a named graph position.

```
?s <http://purl.org/dc/terms/creator> <http://example.com/staff/8574> .
```

SPARQL querying has two main operations.
Graph pattern matching is the first one.

### Graph pattern matching
Graph pattern is a triple (or a set of triples) where some positions are occupied by variables.
In this phase, we try to match the graph pattern to what is in our RDF database. In this case, it is trivial, the RDF database (on the right) consists of a single triple.
The matching operation compares values (IRIs, blank nodes, literals) in the same positions in the triples in the graph pattern to the triples in the database.
A variable matches everything.
If a match is found, we proceed with the next step - phase, variable binding.


### Variable binding
In the variable binding phase, whatever from the database matches the variable, the value is assigned to the variable.
This is done for all variables in the matching graph pattern.
The result is a table of solutions.
Each solution is a possible binding of variables, so that the graph pattern matches.
The table of solutions has columns for variables and rows for their possible bindings.


#### OPTIONAL
If some part of the graph pattern we want to be optional

```
?stud sis:name ?name ; 
      sis:age ?age .
OPTIONAL { 
      ?stud rdf:type ?type. 
}
```

#### UNION
Sometimes OPTINAL can be replaced by UNION (may be faster)

```
{
?stud sis:name ?name ; 
      sis:age ?age .
}
UNION
{ 
?stud sis:name ?name ; 
      sis:age ?age ;
      rdf:type ?type. 
}
```
### Complete example
- WHERE clause contains the graph pattern.
- SELECT clause allows us to get the Solutions table. We can pick some columns of the solutions table, or use “*” here to get all columns.
- we need to define all used prefixes.
- The SPARQL syntax is very similar to RDF Turtle.

```
PREFIX sis: <http://is.cuni.cz/studium/sis#>
SELECT ?name ?age
WHERE {
  ?stud a ?type ;
  sis:name ?name ; 
  sis:age  ?age .
}
```

## Proloque
First part of a SPARQL query
- defines prefixes and base IRI
Like in Turtle, but without @ and without "."

### Prefix
```
PREFIX name: <http://www.my.cz/>
…
WHERE {
   name:local ?p ?o.
}
```


### Relative URIs
```
BASE <http://www.my.cz/>
…
WHERE {
    <sis> <http://www.my.cz/sis> ?o
}

```

## Named graphs
Searches for all named graphs (?g) containing a triple “?s a foaf:Person”.

```
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
SELECT DISTINCT ?g
WHERE {
    GRAPH ?g {

        ?s a foaf:Person .

    }
}
```

Searches for all people ?s in the named graph <https://…>
```
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
SELECT DISTINCT ?s
WHERE {
    GRAPH <https://...> {

        ?s a foaf:Person .

    }
}
```

## Literals
Language tags
- "Praha"
- "Praha"@cs
- "Prague"@en

Type literals
- 1 = "1"^^xsd:integer
- 1.5 = "1.5"^^xsd:decimal
- 1.0E6 = "1"^^xsd:double
- true = "true"^^xsd:boolean

## FILTER
Only solutions matching the logical expression in the FILTER clause gets to the Solutions table.

```
PREFIX sis: <http://is.cuni.cz/studium/sis#>
SELECT ?name ?age
WHERE {
  ?stud a ?type ;
      sis:name ?name ; 
      sis:age  ?age .
    
  FILTER (?age > 27)    
}
```

## Logical expressions
Usual
- Arithmetic operators
    - Unary + – 
    - Binary + – * /
- Comparison operators
    - < <= >= >
    - = !=
- Logical connectives
    - ! && ||

RDF Specific
- Other operators
    - bound(?s): whether a variable is bound (as opposed to not boud like in OPTIONAL or UNION)
    - isIri(?s): whether the variable contains an IRI
    - isBlank(?s): whether the variable contains a blank node
    - isLiteral(?s): whether the variable contains a literal
- Access functions
    - str(?s):  accesses the string value of a literal, e.g. str(“Hello”@en) = “Hello
    - lang(?s): accesses the language tag part of a literal, e.g. lang(“Hello”@en) = “en”
    - dataType(?s): accesses the datatype IRI of a literal with a data type

## Propety paths
way, we can omit creating the intermediate variables.
Instad of
```
PREFIX schema: <http://schema.org/>
PREFIX gr: <http://purl.org/goodrelations/v1#>


SELECT ?check ?fine 
WHERE {
  ?check a schema:CheckAction ;
     schema:result ?sanction .
  ?sanction schema:result ?price .
  ?price gr:hasCurrencyValue ?fine .
} 
LIMIT 100


```
we can write

```
PREFIX schema: <http://schema.org/>
PREFIX gr: <http://purl.org/goodrelations/v1#>

SELECT ?check ?fine 
WHERE {
  ?check a schema:CheckAction ;
     schema:result/schema:result/gr:hasCurrencyValue ?fine .
} 
LIMIT 100

```
- sequences
    - path1/path2
- Alternatives
    - path1|path2
- Groups
    - (path)
- Negation
    - !item
    - !(item1|item2|…)
- Occurrences
    - path*
    - path+
    - path?
- Inverse paths (from object to subject)
    - ^path



## Aggregation
- COUNT
- SUM
- AVG
- MIN
- MAX
- GROUP_CONCAT(?x ; separator="|")
- SAMPLE


```
What was the highest issued fine?
PREFIX schema: <http://schema.org/>
PREFIX gr: <http://purl.org/goodrelations/v1#>

SELECT (MAX (?fine) AS ?max)
WHERE
{
?check a schema:CheckAction ;
   schema:result/schema:result/gr:hasCurrencyValue ?fine .
}

```

## Federated query
Here, from the current SPARQL endpoint we get ?s - an IRI identifying a person.

The name of the person is, however, queried for in another SPARQL endpoint

Like this, one query can use data in multiple SPARQL endpoints.

```
PREFIX foaf: <http://xmlns.com/foaf/0.1/>
SELECT ?s ?name
WHERE {
    ?s a foaf:Person .
   SERVICE <https://peoplenames.org/sparql> {
        ?s foaf:name ?name .
   }
}
```


## BIND
Sometimes we need to compute a value that is not in the data.

```
PREFIX dct: <http://purl.org/dc/terms/>
PREFIX ns: <http://example.org/ns#>

SELECT ?title ?price
WHERE { ?product ns:price ?p ;
                 ns:discount ?discount ;
                 dct:title ?title . 
   BIND (?p * ( 1 - ?discount) AS ?price)
   FILTER(?price < 20)
}
```

## Functions
- if - IF(?x = 2, "yes", "no")
- coalesce
- exists { graph pattern }
- not exists { graph pattern }
- IN, NOT IN

### Functions on RDF terms
- isIRI
- isBlank
- isLiteral
- isNumeric
- str
- lang
- datatype
- IRI - takes a string that looks like an IRI and creates and actual IRI
- STRDT - constructor function for literals
- STRLANG - constructor function for literals
- UUID


### Functions on strings
- STRLEN
- SUBSTR
- UCASE, LCASE
- STRSTARTS, STRENDS
- CONTAINS
- STRBEFORE, STRAFTER
- ENCODE_FOR_URI - when we need to create a URI out of a possibly dangerous (for URIs) string
- CONCAT
- langMatches
- REGEX
- REPLACE


### Functions on numerics
- abs
- round
- ceil
- floor
- RAND

### Functions on dates and times
- now
- year
- month
- day
- hours
- minutes
- seconds
- timezone
- tz

```
tz("2011-01-10T14:45:13.815-05:00"^^xsd:dateTime)
now()
timezone("2011-01-10T14:45:13.815-05:00"^^xsd:dateTime)
```

## Result forms

### SELECT
Result: Solutions table (e.g. in CSV or JSON)

### ASK
Checks whether at least one result item exists
Result: True or false

```
Is there a CTIA inspection with a resulting fine higher than 5 000 000?

PREFIX schema: <http://schema.org/>
PREFIX gr: <http://purl.org/goodrelations/v1#>
PREFIX rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#>
ASK {
?check a schema:CheckAction ;
   schema:result/schema:result/gr:hasCurrencyValue ?fine .
FILTER(?fine > 5000000)
}
```

### CONSTRUCT
Result: RDF graph constructed from a template.

```
CONSTRUCT
{ ?s sis:name ?fullName }
WHERE {
  ?s sis:firstName ?n1 ;
     sis:lastName ?n2 .
  BIND(STRLANG(CONCAT(?n1, " ", ?n2), "cs") AS ?fullName)
}
```

### DESCRIBE
Result: RDF graph about the given resource.
Specification non-normative - various triplestores implement it differently.

```
DESCRIBE <http://www.my.cz/>
```

### SELECT modifiers

#### ORDER BY
- Orders items in the solutions table
- Hierarchical ordering criteria
    - ASC = ascending (default)
    - DESC = descending
- Unbound variable < blank node < URI < literal

```
PREFIX     :  <http://example.org/ns#>
PREFIX foaf:  <http://xmlns.com/foaf/0.1/>

SELECT ?name
WHERE { ?x foaf:name ?name ; 
        :empId ?emp }
ORDER BY ?name DESC(?emp)
```

##### LIMIT
- Limits the number of items in the result sequence
- Always should be preceded by ORDER BY modifier
- Because RDF graph is a set with no ordering
- Used as page size
```
ORDER BY ?name LIMIT 10
```
#### OFFSET
- Index of the first reported item from the sequence
- Used for paging through results
```
ORDER BY ?name LIMIT 10 OFFSET 20
```

#### GROUP BY and HAVING

```
PREFIX : <http://data.example/>
SELECT (AVG(?size) AS ?asize)
WHERE {
  ?x :size ?size
}
GROUP BY ?x
HAVING(AVG(?size) > 10)
```