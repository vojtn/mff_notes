# JSON Schema
https://json-schema.org/
- Proposed IETF/ECMA standard
“JSON Schema is a vocabulary that allows you to annotate
Roles:
- annotation - describing the structure for people (title, description)
- validation - constraining the structure for machines (type)
First proposal: 2007
Still under development, currently 2020-12

```
{
    $schema": "https://json-schema.org/draft/2020-12/schema",
    "$id": "http://example.com/product.schema.json",
    "title": "Product",
    "description": "A product in the catalog",
    "type": "object"
}
```

## Properties

```
"properties": {
      "productId": {
        "description": "The unique identifier for a product",
        "type": "integer"
      },
      "productName": {
        "description": "Name of the product",
        "type": "string"
      }
    },
    "required": [ "productId", "productName" ]
```

## Numerical constraints
Validation keywords for numeric instances
- multipleOf
- maximum, exclusiveMaximum
- minimum, exclusiveMinimum


## Arrays

Validation keywords for arrays - list validation
items, maxItems, minItems
contains, maxContains, minContains
uniqueItems


## String contraints 
Length
```
{
    "type": "string",
    "minLength": 2,
    "maxLength": 3
}

```

Regular expression
```
{
    "type": "string",
    "pattern": "^(\\([0-9]{3}\\))?[0-9]{3}-[0-9]{4}$"
}
```

## Formats
built-in formats for strings
- date-time, date, time, duration
- email, idn-email
- hostname, idn-hostname
- ipv4, ipv6
- uri, uri-reference
- iri, iri-reference
- uuid
- uri-template
- json-pointer, relative-json-pointer
- regex

```
"typ_turistického_cíle": {
    "type": "string",
    "format": "iri",
    "pattern": "^https\\://data\\.dia\\.gov\\.cz/zdroj/číselníky/typy-turistických-cílů/položky/.*$",
    "title": "Typ turistického cíle",
    "examples": [ 
        "https://data.dia.gov.cz/zdroj/číselníky/typy-turistických-cílů/položky/přírodní"
    ]
}
```

### Boolean
```
{ "type": "boolean" }

```

### Null
```
{ "type": "null" }

```

### Combining schemas
Schemas can be combined:
- anyOf
    - valid against at least one schema
- allOf
    - valid against all schemas
    - can be used for extending schemas
- oneOf
    - valid against exactly one schema
- not
    - valid against none of the schemas

```
"anyOf": [
    { "type": "string", "maxLength": 5 },
    { "type": "number", "minimum": 0 }
]
```

### Validator
https://www.jsonschemavalidator.net/
https://tryjsonschematypes.appspot.com/#validate

## JSON-LD
Goal of JSON-LD is to satisfy both JSON and RDF oriented developers.

JSON-LD @context

Makes JSON interpretable as RDF model through mapping specified by @keywords

RDF oriented developers can load a JSON-LD file just as any other RDF serialization
JSON oriented developers can ignore @context and work with the rest of the file as with a regular JSON file

JSON-LD 1.1 - W3C Recommendation
- 16 July 2020


```
{
  "@context":
  {
    "name": "http://schema.org/name",
    "image": {
      "@id": "http://schema.org/image",
      "@type": "@id"
    },
    "homepage": {
      "@id": "http://schema.org/url",
      "@type": "@id"
    }
  },
    "name": "Manu Sporny",
    "homepage": "http://manu.sporny.org/",
    "image": "http://manu.sporny.org/images/manu.png"
}


```
