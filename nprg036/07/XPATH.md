# XML Path Language - XPath
- XML Path Language (XPath) 1.0
    - W3C Recommendation 1999
    - what we will cover mostly
- XML Path Language (XPath) 2.0 (Second Edition)
    - W3C Recommendation 2010
    - most widely implemented
- XML Path Language (XPath) 3.1
    - W3C Recommendation 2017

## Example

```
/catalog/datasets/dataset/title
/catalog/datasets/dataset/title/text()
/catalog/datasets/dataset/title[@xml:lang="en"]/text()
```

## XML Infoset
XML Information Set (Second Edition)
- W3C Recommendation (Second Edition) 2004
- Set of definitions for referring to information in well-formed XML documents
- Created with no particular processing language in mind

## Data model
XQuery and XPath Data Model 3.1
- W3C Recommendation 2017
    - For XPath 2.0 2001
- Based on XML Infoset
- Created for use in XPath, XSLT and XQuery 
- Includes support for information coming from XML Schemas
    - e.g. types of text values

### Node types
- document (root)
- element
- attribute
- text
- comment
- namespace
- processing instruction

### Principles

#### Absolute path 
/step1/.../stepN

#### Relatice path
title[@xml:lang="en"]/text()

step1/.../stepN
Needs a starting point


#### Result 
set of nodes (no explicit order)

#### Access function 
text()

#### Attribute
@attribute ... /catalog/datasets/dataset/title/@xml:lang 

#### Predicates
/catalog/datasets/dataset/title[@xml:lang="en"]/text()

(predicate filters the current set of nodes only to those, for which the expression evaluates to true
)


### Axes
- ancestor
- parent
- preceding-sibling
- preceding
- self
- child
- following-sibling
- following
- descendant

## Document order
according to the position of start tags of elements.

## XPath 2.0 features
- result is a sequence (ordered)

- conditional expressions
```
if (count(//dataset) > 1) then "Datasets" else "Dataset"

//dataset[some $title in title satisfies $title/@xml:lang="en"]
```
- for cycles
```
for $dataset in //dataset return count($dataset//distribution)
```

## XPath 3.0/3.1 features
- mapping operator !

- string concatenation operator ||

- functions chaining (to avoid deep nesting)