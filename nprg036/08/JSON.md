# JSON (JavaScript Object Notation)
- light-weight
- language independent
- easy to read and write by humans
- easy to parse and generate by machines
- used as serialization in 100+ media types
Media type: application/json  
File extension: .json  
Specific formats: …/…+json  
e.g. application/activity+json  
 
Example:
```
{
    "Image": {
        "Width": 800,
        "Height": 600,
        "Title": "View from 15th Floor",
        "Thumbnail": {
            "Url": "http://www.example.com/image/481989943",
            "Height": 125,
            "Width": 100
        },
        "Animated": false,
        "IDs": [
            116,
            943,
            234,
            38793
        ]
    }
}

```
## Tools
JSONLint: https://jsonlint.com/  
Schema Validator: https://www.jsonschemavalidator.net/  
JSON-LD Playground: https://json-ld.org/playground/  
JQ: https://play.jqlang.org/ 

## String
unicode (utf-8)
\ escapes

Correct examples:
```
"View from 15th Floor"
"View from \"15th Floor\""
"This is a \n multiline string"
"\u004a\u0053\u004f\u004e String"
```

Incorrect examples:
```
"This is not a 
multiline string"
"View from "15th Floor""
```
## Number
No octal or hexadecimal digits, decimal only
Correct:
```
0
1
-1
42
3.14
```
Incorrect:
```
3,14
3/5
"24"
```
## Whitespace
Used for indentation
- space
- linefeed
- carriage return
- horizontal tab

## Value
whitespace + x + whitespace
x:
- string
- number
- object
- array
- true
- false
- null

## Array
ordered collection of values
- starts with [
- ends with ]
- values separated by ,
```
[
    116,
    943,
    "test",
    null
]
```
- can be used as a value
- can also be root of JSON file
- can contain values of different types

## Object
- unordered set of name/value pairs
- starts with {
- ends with }
- name and value separator :
- individual name/value pairs separated by ,
- no , after the last one before } 

```
{
    "Width": 800,
    "Height": 600,
    "Title": "View from 15th Floor"
}
```
- can be used as a value
- can also be root of JSON file

## Specification
- 1999: ECMA-262, 3rd Edition, ECMAScript Language Specification
- 2001: json.org
- 2006: RFC 4627, The application/json Media Type for JavaScript Object Notation (JSON)
- 2013: ECMA-404, 1st edition, The JSON Data Interchange Standard
- 2014: RFC 7158, RFC 7159 The JavaScript Object Notation (JSON) Data Interchange Format
- 2017: ECMA-404, 2nd edition, The JSON Data Interchange Standard
- 2017: RFC 8259 The JavaScript Object Notation (JSON) Data Interchange Format


## Syntax check
- [jsonlint](https://jsonlint.com/)
- [jsonformatter](https://jsonformatter.curiousconcept.com/#)

## Usage

### Web APIs
GitHub: https://api.github.com/repos/stedolan/jq/commits?per_page=5

### Data standards
Standard for Czech Touristic Points of Interest: https://ofn.gov.cz/turistické-cíle/2020-07-01/


### jq
- coommand-line JSON query tool
supports filters
- .[0] - selects first item in a JSON array
- | passes into the next filter
- { } - constructs a JSON object

```
jq '.[0] | {message: .commit.message, name: .commit.committer.name}'
```

### Document stores
Apache CouchDB - allows read, update and delete of JSON documents (document database)

### Indices
Apache Solr - allows searching in JSON fields

### JSON Lines
https://jsonlines.org/
- each line is a valid JSON Value
- alternative to a directory of individual JSON files
- alternative to CSV files
File extension: .jsonl  
Stream compression recommended  
.jsonl.gz .jsonl.bz2  
- Mainly for processing record by record


```
{"name": "Gilbert", "wins": [["straight", "7♣"], ["one pair", "10♥"]]}
{"name": "Alexa", "wins": [["two pair", "4♠"], ["two pair", "9♠"]]}
{"name": "May", "wins": []}
{"name": "Deloise", "wins": [["three of a kind", "5♣"]]}
```

### XSLT 3.0 json-to-xml()
The XML representation according to the XML schema can be also used for reverse transformation  
The XML array for London is omitted.

fn:json-to-xml($json-text as xs:string) as document-node()

fn:xml-to-json($input as node()?) as xs:string?

### JSON Pointer
RFC 6901
- ability to point to an arbitrary value in a JSON document
- pointer representation as JSON string or URI fragment

```
/uptodate
/cities/London
/cities/Brussels/0/to
```

```
https://example.org/my.json#/cities/Brussels/0/to
```
