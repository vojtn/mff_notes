# Data
Necessity of correct data representation and following specifications
- Data should be app-independent -> apps do operations on top of the data
- multiple app may need to share


## Conceptual domain model
What is the data about

Conceptual model -> logical model -> physical level
- independent of any representation or technology
- can be discussed with non-IT people

Consists of:
- Class
- Attribute
- Association

## Data models
Logical view of the data - how is data structured using given technology/format
(tools/shapes for representing our data)
1. Graphs
    - RDF model
    - LPG mdel 
2. Hiearchies
    - DOM (Document Object Model)
    - JSON (both format and model)
3. Tables
    - Relation model

## Data formats
How data using a certain data model are serialized
physical level - how do the files look like in storage

1. Graph
    - RDF graph model
        - Text-based: N-Triples, N-Quads, Turtle, TriG, RDF/XML, JSON-LD, RDFa
        - Binary: HDT
    - Property graph 
        - CSV, JSON, GraphML, Cypher Script
2. Hierarchical
    - DOM
        - XML, HTML
    - JSON
        - JSON, XML
3. Relational
    - CSV, SQL dump


### Schemas
Annotations and constraints applicable to instances of data formats, allowing the data to be better described and validated

- CSV
    - CSV on the web
- RDF
    - SHACL
    - ShEx
- JSON
    - JSON schema
- XML
    - DTD
    - XML schema
    - Relax NG

### Specific data formats
metaformats = CSV, XML, JSON = hosts formats for use-case specific format

JSON
- GeoJSON
CSV
- GTFS

XML
- SVG
- Atom
- RSS
- Office Open XML

RDF
- DCAT

### Properties

#### Open
Specification available on the Web, freely accessible to anyone, with no limitation on its usage.
- Meta-formats e.g.: XML, JSON, CSV, RDF
- Specific formats: SVG, GeoJSON, ...

#### Closed
- specification not accessible
- need for payment for access to specification
- need for registration
- need for certification of library/application claiming compatibility

e.g. railML.org
- XML based
- need for certification

#### Machine-readable
- Machine readability is not a property of a format
- Depends on the form of a particular data instance
Says whether the data is *easily processed* by appropriate applications

#### Binary formats
- their structure may be defined on bit by bit level
- a.k.a. “non-text” file
- Not readable by text editors
- Viewable by hex editors

#### Text-based formats
- Contains text
- Typically structured as characters on lines
- Viewable by text editors
- Also viewable by hex editors
- Text is encoded into 1s and 0s using character encoding

##### Character encoding
###### ASCI
Character encoding - representation of characters as binary sequences (numbers)
US-ASCII using 7 bits to represent 1 character

###### New line representation
- CR - carriage return - \r
- LF - line feed - \n - Unix/Linux, MacOS
- CR LF - both of them - \r\n - Windows

###### UTF-8
- 1 to 4 bytes representing one character
- first byte compatible with US-ASCII
- most frequently used characters use 2 bytes
- emojis use 4 bytes


###### BOM (Byte order mark)
Magic number at the beginning of a text file
Indicates
1. unicode encoding
2. coding type
    - UTF-8 - EF BB BF
    - UTF-16 BE - FE FF
    - UTF-16 LE - FF FE
    - UTF-32 00 00 FE FF
    - more...
3. byte order (endianness) for multi-byte encodings

Most data formats use UTF-8 without BOM, cause other variants are rarely used on the Web

###### Other
From Czech legacy systems
1. iso-8859-2 (Latin 2)
2. windows-1250


## Standardization
Needed for interoperability 
but also for business, so it is clear who is doing something wrong

### IETF (Internet Engineering Task Force)
Open standards organization
- founded 1986
- initially supported by the US federal government
- now under ISOC
- participants are volunteers
IETF Working Groups
- topic, chairperson, charter, focus, deadline
- open to all
Internet Engineering Steering Group (IESG)
- final technical review of Internet standards

### ISOC (Internet Society)
American non-profit
- founded 1992
- to provide leadership in Internet-related standards, education, access, and policy
- deals mainly with political issues
- standards are created by the Internet Engineering Task Force (IETF) to which ISOC is related
- RFC - Request for Comments -> some become Internet Standards

"to promote the open development, evolution, and use of the Internet for the benefit of all people throughout the world”

### W3C (World Wide Web Consortium)
International standards organization for the WWW
- founded 1994
- by Tim Berners-Lee - inventor of the Web
- issues Recommendations
e.g. HTML, CSS, RDF, XML, RSS…
Specification maturation process
1. Working draft (WD): ideas collected by editors, public can comment
2. Candidate recommendation (CR): specification achieves goals. Developers comment on how implementable it is
3. Proposed recommendation (PR): specification has implementations, is being tested
4. W3C recommendation (REC): specification is finished, tested practically, wide public should adopt it
- membership is paid and must be approved
    - universities, non-profits, businesses, governments, individuals

### ICANN (Internet Corporation for Assigned Names and Numbers)
Standards organization
- founded 1998
- manages IANA - Internet Assigned Numbers Authority
- IPv4 and IPv6 address space management
- autonomous system number allocation
- root zone management in DNS
- media types

### MIME-type
Multipurpose Internet Mail Extensions (MIME) type
Managed by
Internet Assigned Numbers Authority (IANA)
Examples:
- text/html
- text/xml
- application/xml
- application/soap+xml
    + suffix - specifies serialization - e.g. +xml, +json, +zip
- application/vnd.openxmlformats-officedocument.wordprocessingml.document
    - vnd. - publicly available products, e.g. Microsoft Office
text/x-turtle

### ECMA International
Standards organization
- founded 1961
- membership-based
- IT companies, IT trade associations, universities, foundations and public institutions
- rebranded in 1994 from European Computer Manufacturers Association (ECMA)
HQ: Geneva, Switzerland

Examples:
- ECMA-262 – ECMAScript Language Specification (based on JavaScript)
- ECMA-334 – C# Language Specification
- ECMA-376 – Office Open XML
- ECMA-404 – JSON

### Requerements levels
Keywords in RFC:
- must, required, shall: absolute requirement
- must not, shall not: absolute prohibition
- should, recommend: there may exist valid reasons in particular circumstances to ignore a particular item
- should not, not recommended: there may exist valid reasons in particular circumstances when the particular behavior is acceptable or even useful

## Indentifiers

### URI (Uniform Resource Identifier)
RFC 3986
- allows unicode in the path

### URN (Uniform Resource Name)
RFC 8141

### URL (Uniform Resource Locator)
RFC 3986

```
ftp://ftp.is.co.za/rfc/rfc1808.txt
http://www.ietf.org/rfc/rfc2396.txt
ldap://[2001:db8::7]/c=GB?objectClass?one
mailto:John.Doe@example.com
```


### IRI (Internationalized Resource Identifier)
RFC 3987
Percent-encoding
- For some usages only URIs are acceptable - e.g. HTTP
- IRIs are encoded in URIs
- each byte represented as '%' and two hexadecimal digits e.g. 💩 => %F0%9F%92%A9

example: https://opendata.gov.cz/špatná-praxe:start

### Punycode
Special encoding used to convert Unicode characters to ASCII, which is a smaller, restricted character set.
- used to encode internationalized domain names (IDN).
- RFC 3492 
IRIs not to be confused with IDN - internationalized domain name:

```
https://www.háčkyčárky.cz = https://www.xn--hkyrky-ptac70bc.cz/
```
- even less readable than percent-encoding
- punycoded name is used with DNS


## Data types
Common data types in all commons formats like RDF syntaxes, XML, JSON, CSV based on XML schema data type system

- boolean
    - true
    - false
- number
    - integer
    - decimal
    - float/double
- date (ISO-8601)
    - YYYY-MM-DD
- time
    - HH:MM:SS.sss
- dateTime
    - YYYY-MM-DDTHH:MM:SS.sss
- timeZones
    - 2021-03-01T10:40:00+02:00
    - 2021-03-01-02:00
    - 2021-03-01Z (Z = UTC)