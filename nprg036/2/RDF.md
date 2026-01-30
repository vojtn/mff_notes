
# Graph data representation
There is a thing, which is a catalog = statement or triple

ex:catalog rdf:type dcat:Catalog .

The catalog has title “my catalog”

ex:catalog dcterms:title "my catalog" .

The original sentences can be represented as data, based on the graph representation.

- IRIs are too long -> use their prefixes.


# RDF (Resource Description Framework)
- Graph based data model
- set of triples, which describes a relation  (subject, predicate, object)
- 2004 & 2014 W3C Recommendations

```
<http://example.com/index.html> <http://purl.org/dc/terms/creator> <http://example.com/staff/8574> .
```

Subject (S) = <http://example.com/index.html>
Predicate (P) = <http://purl.org/dc/terms/creator>
Object (O) = <http://example.com/staff/8574>

With meaning: 
The example page (identified by http://example.com/index.html) was created by (http://purl.org/dc/terms/creator) employee number 8574 (identified by http://example.com/staff/8574).

## Serialization
RDF serialization is a representation of the RDF data model in a (text) file
7 Standardized for RDF 1.1:
- RDF/XML
- RDFa
- N-Triples
- Turtle
- JSON-LD
- N-Quads
- TriG

## Resource
A resource is anything identified by an IRI.

## Prefix
<http://purl.org/dc/terms/creator>
=
@prefix dcterms: <http://purl.org/dc/terms/> .
dcterms:creator

## Data model
RDF data model is a set of triples -> no order 

### Literal values

```
<http://example.com/index.html> <http://purl.org/dc/terms/subject> "education" .
```

### Type
A literal value needs to have its datatype specified. If not, xsd:string is assumed.
The datatype is specified using an IRI of the datatype.
The datatype system is reused from the XML Schema definition,

### Language
if it has a text in natural language, needs to have this language specified by a language tag.

```
my:index.html dcterms:title "Homepage of Jakub Klímek"@en .
```


### Classes
Classes are Resources.
- We can say that a resource is of a type (rdf:type) represented by the Class.
- rdf:type is a well-known predicate (specified in RDF) for stating this.

```
my:staff/85740 rdf:type my:Person
```
In this example, we have an employee (identified by my:staff/85740) and we say that they are a person (a class identified by my:Person).
It is usually the first statement we make about every Resource in RDF.


### Blank node 
Resource like any other - can be used as object in one statement and as subject in another.
However, it is not identified by an IRI.

It has a “node ID” (a1 in this case), which is valid only within one document.

```
my:staff/85740 my:hasAddress _:a1 .
_:a1 my:street "Malostranske nam. 25" .
_:a1 my:city "Prague" .
_:a1 my:zipCode "11800" .ple
```

### Statements about statements 
```
my:index.html my:createdBy "Jakub Klímek" .
```
The statement itself does not have an identifier - we cannot say anything about it.
How to represent 
1. came from https://x.y.z
2. was scraped on 2020-04-23

#### Reification
Direct approach:
- Statement will become a resource.
- Assign IRI to the statement itself, or
make it a blank node (e.g. _:triple1)
Original statement:
```
my:index.html my:createdBy "Jakub Klímek" .
```
Reified statement:
```
_:triple1 a rdf:Statement .
_:triple1 rdf:subject	my:index.html	.
_:triple1 rdf:predicate	my:createdBy	.
_:triple1 rdf:object	"Jakub Klímek"	.
```

#### Named Graphs
Alternative approach to the problem:
- Statements belong to “named graphs”
- Named graphs are resources
- We can state facts about resources

RDF Triples become RDF Quads
- S P O G
- G can be used as subject of another triple (quad)
```
(S) <http://example.org/#spiderman> 
(P) <http://www.perceive.net/schemas/relationship/enemyOf> 
(O) <http://example.org/#green-goblin> 
(G) <http://example.org/graphs/spiderman> .
```

#### RDF dataset 
Consists of 
- set of named graphs (identified by IRIs)
- one default graph

{default graph, https://example.org/named-graphs/1, https://example.org/named-graphs/2}

# RDF Serializations
Representation of the RDF data model in a (text) file

## N-Triples
The easiest serialization. All of its possibilities are shown on this one slide.

Pros:
- Easy to parse, easy to write
- Can be streamed (even compressed by stream compression techniques such as GZIP)
- Can be paged easily (except for blank nodes)
Cons:
- hard to read by humans
- large in size (uncompressed)

```
<http://example.com/index.html> <http://purl.org/dc/terms/created> "2020-04-23"^^<http://…#date>  .
<http://example.com/index.html> <http://purl.org/dc/terms/creator> <http://example.com/staff/8574>  .
<http://example.com/index.html> <http://purl.org/dc/terms/creator> <http://example.com/staff/8575>  .
<http://example.com/index.html> <http://purl.org/dc/terms/title> "Moje stránka"@cs  .
<http://example.com/index.html> <http://purl.org/dc/terms/title> "My page"@en  .
```

## RDF Turtle
uses prefixes
- It shortens the IRIs
- Makes IRIs more legible for people - people get used to prefix names much better than parsing IRI prefixes

```
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .
@prefix dcterms: <http://purl.org/dc/terms/> .
@prefix my: <http://example.com/> .
@prefix staff: <http://example.com/staff/> .

my:index.html dcterms:created "2020-04-23"^^xsd:date  .
my:index.html dcterms:creator staff:8574  .
my:index.html dcterms:creator staff:8575  .
my:index.html dcterms:title "Moje stránka"@cs  .
my:index.html dcterms:title "My page"@en  .
```
### Semicolon
Semicolon means, that we continue with describing the same subject.

```
my:index.html dcterms:created "2020-04-23"^^xsd:date  ;
              dcterms:creator staff:8574  ;
              dcterms:creator staff:8575  ;
              dcterms:title "Moje stránka"@cs  ;
              dcterms:title "My page"@en  .
```
### Comma
Comma means, that next we specify an RDF triple with the same subject and the same object.
This can be viewed as a list (unordered) of values for a given property of a given subject.

```
my:index.html dcterms:created "2020-04-23"^^xsd:date  ;
              dcterms:creator staff:8574  ,
                              staff:8575  ;
              dcterms:title "Moje stránka"@cs  ,
                            "My page"@en  .
```

### Prefixes
1. "no-name" prefix (used as :bar)
2. constant (with no suffix) (foo:)
3. noname can be used with no suffix (:)

```
@prefix foo: <http://example.org/ns#> . # contant
@prefix : <http://other.example.org/ns#> .  ## no0name
foo:bar foo: : .
:bar : foo:bar .
```
meaning
```
<http://example.org/ns#bar> <http://example.org/ns#> <http://other.example.org/ns#> .

<http://other.example.org/ns#bar> <http://other.example.org/ns#> <http://example.org/ns#bar> .
```

### Multiline strings
"""a string
with newlines
"""

### Escape sequences
- \t (U+0009, tab)
- \n (U+000A, linefeed)
- \r (U+000D, carriage return)
- \" (U+0022, double quote - only allowed inside strings)
- \> (U+003E, greater than - only allowed inside URIs)
- \\ (U+005C, backslash)
- \uHHHH or \UHHHHHHHH for writing Unicode characters by hexadecimal codepoint where H is a single hexadecimal digit.

### Class assignment
Syntactic shortcut. 
rdf:type is shortened as “a”.
This is because a statement like this one reads as: “Page is a Document”
```
<http://example.com/index.html> <http://www.w3.org/1999/02/22-rdf-syntax-ns#type> foaf:Document .
```
=
```
<http://example.com/index.html> a foaf:Document .
```

### Blank nodes
Another syntactic shortcut.
This time, we do not have to specify the node ID of a blank node, if we use "[ ]".

### Datatype shortcuts
Equivalent statements
```
ex:Car ex:numberOfWheels 4 ;
ex:Car ex:numberOfWheels +4 ;
ex:Car ex:numberOfWheels "4"^^xsd:integer ;
```

```
ex:Car ex:value 1300000.0 ;
ex:Car ex:value "1300000.0"^^xsd:decimal ;
```

## N-Quads
Based on N-Triples, adds support for [named graphs](#named-graphs)

S P O G
```
<http://example.org/#spiderman> <http://www.perceive.net/schemas/relationship/enemyOf> <http://example.org/#green-goblin> <http://example.org/graphs/spiderman> .
```

## TriG
RDF Dataset consists of
- 1 default graph
- N named graphs

```
@base <http://www.w3.org/People/> .
@prefix : <http://xmlns.com/foaf/0.1/> .

# default graph
{
     ericFoaf:ericP :givenName "Eric" .
}

# also default graph, no {}
ericFoaf:ericP :givenName "Eric" .

# graph highlight
GRAPH <Eric/ericP-foaf.rdf> {
	ericFoaf:ericP :givenName "Eric" .
}
```