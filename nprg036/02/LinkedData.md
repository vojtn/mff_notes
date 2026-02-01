# Open World Assumption (OWA)
“open-world assumption is the assumption that the truth value of a statement may be true irrespective of whether or not it is known to be true”

```
Statement: "Mary" "is a citizen of" "France"
Question: Is Paul a citizen of France?

"Closed world" (for example SQL) answer: No.
"Open world" answer: Unknown.
```

# Linked data
Regular data are not linked
issues:
- different formats
- lack of unique identifiers
- no specified location
- unclear meaning (no context)
- linking

## WWW principles
- Publish human-readable documents
- Everyone can view them in their browser
if they know the URL
- links 
    - To documents with yet unknown URL
    - From other documents
    - From catalogs
- Fulltext search, keyword search
Author: Sir Tim Berners-Lee

1. HTML as a format for publishing documents
2. URLs as unique global identifiers of documents
3. HTTP for localization and accessing documents by their URLs
4. hyperlinks between documents


## Linked data = web of data
principles and best practices for publishing and linking data about entities on the Web

application of the proven priciples of web of Documents to data
2 main goals:
1. machine readable
2. providing context

## Principles
1. Use URIs as names for things.
2. Use HTTP URIs so that people can look up those names.
3. When someone looks up a URI, provide useful information, using the standards (RDF, SPARQL).
4. Include links to other URIs so that they can discover more things.

## Web of documents and Web of data comparision

| Web of documents | Linked Data |
| - | - |
| HTML as document publication format | RDF as a data publication format |
| URL as a unique global document identifier | URL as a unique global entity identifier |
| HTTP protocol for accessing documents using their URL | HTTP protocol for accessing data about entities using their URL |
| Links to other documents |Links to other entities |
| | vocabularies – standards for common data representation |

## Linked Open Data
Best technical way of representing open data -> many datasets

1. Open (free to use, reuse, and share)
2. Published on the Web
3. Structured using standard formats (RDF)
4. Interlinked with other datasets using URIs.

examples:
- DBpedia
- Wikidata