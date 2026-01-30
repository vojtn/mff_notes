# Tagged message
- contains tags inside text message
- allows the users, both human and machine to query the document for important pieces of information.
- At the same time, the document is still human readable when the XML tags are omitted.

# Document-oriented XML
- root element
- XML prolog
- It was created manually, by tagging
- It is irregular
- Still mainly human readable document
- similar to HTML

```
<?xml version="1.0" encoding="UTF-8"?>
<message>
Dear <customer><firstName>John</firstName> <lastName>Doe</lastName></customer>,

the balance on your bank account <accountNumber>111333444/1123</accountNumber> as of <balanceDate>3rd of January 2021</balanceDate> is <balance><value>25000</value> <currency>CZK</currency></balance>.

Best regards,

<bankName>Your bank</bankName>
<streetAddress>1234 5th Avenue</streetAddress>
<phone>+420123456789</phone>
</message>
```

# Data-centric XML
- typically created and consumed by applications, generated from a database or a form
- regularly structured
- no longer human readable when tags are omitted
- typically does not contain mixed content - text mixed with XML elements


# XML (Extensible Markup Language)
- text-based hierarchical format - it needs a root
Differences between versions deal mainly with Unicode
1.0 used widely, 1.1, unfortunately, not so much

## Versions
1. Extensible Markup Language (XML) 1.0
    - W3C Recommendation, First edition, 1998
    - widely adopted
    - element and attribute names use Unicode 2.0 and list permitted characters
2. Extensible Markup Language (XML) 1.1
    - W3C Recommendation, Second edition, 2006
    - not so widely adopted
    - element and attribute names use Unicode and list forbidden characters
    -  Therefore unicode version independent
3. Extensible Markup Language (XML) 1.0 (Fifth Edition)
    - W3C Recommendation, Fifth edition, 2008
    - relaxes element and naming restrictions (towards XML 1.1)


## Example
```
<?xml version="1.0" encoding="UTF-8"?>
<!-- XML declaration -->
<!-- root element -->
<root-element>
   <!-- an empty element -->
   <element/>
   <!-- attributes of an element -->
   <element attribute1="value"
            attribute2="another value">...</element>
   <!-- an element with subelements -->
   <element attribute1="value" attribute2="value">
    <subelement>TEXT CONTENT</subelement>
    <subelement>...</subelement>
   </element>
</root-element>
```

## Strucure

### Prolog
- version (1.0 or 1.1)
- encoding (UTF-8, ...)

```
<?xml version="1.0" encoding="UTF-8"?>
```

### Root element
Only one root element
```
<root-element>
```
#### Start tag
case-sensitive

```
<element>
```
#### Attributes
unordered, case-sensitive, unique within tag

```
<element attribute1="value"
            attribute2="another value">...</element>
```

#### End tag
“/” at the beginning

```
</root-element>
```

#### Comments
```
<!-- comment -->
```

#### Nested elements
Nested elements subelements, ordered
```
<element attribute1="value" attribute2="value">
    <subelement>TEXT CONTENT</subelement>
    <subelement>...</subelement>
</element>
```

#### Empty element
```
<element/>
```


## Mixed content
Mixed content is a sequence of text nodes and elements

```
<?xml version="1.0" encoding="UTF-8"?>
<message>
Dear <customer><firstName>John</firstName> <lastName>Doe</lastName></customer>,

the balance on your bank account <accountNumber>111333444/1123</accountNumber> as of <balanceDate>3rd of January 2021</balanceDate> is <balance><value>25000</value> <currency>CZK</currency></balance>.

Best regards,

<bankName>Your bank</bankName>
<streetAddress>1234 5th Avenue</streetAddress>
<phone>+420123456789</phone>
</message>
```

## Common syntax errors
- Case mismatch
- missing ending tag
- wrongly nested elements
- more than 1 root elements

## Well-formedness
XML document is well-formed iff it complies with XML syntax rules.
 



## Namespaces
https://www.w3schools.com/xml/xml_namespaces.asp



### QName
```
<h:table xmlns:h="http://www.w3.org/TR/html4/">

```
### Default

```
<root xmlns="http://www.w3.org/TR/html4/">
```

## CDATA sections
Everything between <![CDATA[ and ]]> is treated as string
- for better escaping

```
<?xml version="1.0" encoding="UTF-8"?>
<elementA>
    <![CDATA[<greeting>Hello, world!</greeting>]]> 
</elementA>

```

## Language specification
xml:lang attribute
Language tags specified by IETF BCP 47
consisting of
- RFC 4646: Tags for Identifying Languages
- RFC 4647: Matching of Language Tags

```
<?xml version="1.1" encoding="UTF-8"?>
<document>
    <p xml:lang="en">The quick brown fox jumps over the lazy dog.</p>
    <p xml:lang="en-GB">What colour is it?</p>
    <p xml:lang="en-US">What color is it?</p>
    <sp who="Faust" desc='leise' xml:lang="de">
        <l>Habe nun, ach! Philosophie,</l>
        <l>Juristerei, und Medizin</l>
        <l>und leider auch Theologie</l>
        <l>durchaus studiert mit heißem Bemüh'n.</l>
    </sp>
</document>
```

## XML processing

```
<?xml version="1.0" encoding="UTF-8"?>
<consumers>
    <consumer>
        <name>John</name>
        <drinks>
            <coffee-type when="morning">V60</coffee-type>
            <coffee-type when="after lunch">Batch brew</coffee-type>
            <coffee-type when="afternoon">Flat white</coffee-type>
        </drinks>
        <age>20</age>
        <coffees-per-day>2</coffees-per-day>
    </consumer>
    <consumer>
        <name>Jane</name>
        <drinks>
            <coffee-type when="morning">Aeropress</coffee-type>
            <coffee-type when="after lunch">Cappuccino</coffee-type>
            <coffee-type when="afternoon">Double espresso</coffee-type>
        </drinks>
        <age>18</age>
        <coffees-per-day>1</coffees-per-day>
    </consumer>
</consumers>
```

### DOM (Document object model)
Loads the entire XML document into memory
-does not work for streams
-does not work for large files
+supports arbitrary querying
(a.k.a. random access)
e.g. XPath /consumers/consumer[1]/name

### SAX (Simple API for XML)
Processes the XML file as a stream of events
+works for streams
+works for large files
-does not support effective arbitrary querying (a.k.a. random access)
SAX parser pushes events to your code - until it reads the whole file

SAX parser pushes events to your code:
1. Element start (name = "consumers")
2. Element start (name = "consumer")
3. Element start (name = "name")
4. Text value (value = "John")
5. Element end (name = "name")
6. Element start (name="drinks")
7. Element start (name="coffee-type")
8. Attribute (name="when" value="morning")
9. Text value (value="V60")
10. Element end (name="coffee-type")
...


### StAX (Streaming API for XML)
Processes the XML file as a stream of events
+works for streams
+works for large files
-does not support effective arbitrary querying (a.k.a. random access)
Your code pulls events from the StAX parser - you can stop processing when done


## Posibilities
This is one of the key differences between the XML world and the JSON world in the hierarchical data formats.
XML is a large ecosystem built on rigorous standardization with lots of features for various use cases.
JSON is simple and young - a serialization of an object model of a program (in JavaScript), lacks support of standards.
That is why XML is mostly found in dependable applications - eGovernment, Enterprises.
JSON is used on the Web.


### Explitation
Definition of specific formats

### Parsing
- DOM
- SAX
- StAX
- LINQ

### Validation
- XML Schema (XSD)
    - most wide-spread
- RelaxNG (out of scope)
    - XSD alternative
- DTD (out of scope)
    - basically deprecated
- Schematron (out of scope)
    - rule-based validation
### Querying
- XPath
- XQuery (out of scope)

### Transformation
- XSLT

### Persistance
- XML databases (out of scope)
- SQL/XML (out of scope)

### Message transfer
- Web services (SOAP, WSDL)


### RDF/XML
The oldest RDF serialization

## Specific formats

### SVG
Scalable Vector Graphics (SVG) 1.1 (Second Edition)
- W3C Recommendation 2011
Scalable Vector Graphics (SVG) 2
- W3C Candidate Recommendation 2018


### OOXML
ECMA-376 Office Open XML
ISO/IEC 29500
5th edition, December 2016
.docx, .xlsx, .pptx, …
Zipped XML format

### Atom, RSS
RFC 4287 - The Atom Syndication Format

for web feeds
Alternative to:
- RSS 0.9, 1.0, 1.1
    - RDF Site Summary
    - based on early RDF/XML draft
- RSS 2.x
    - Really Simple Syndication
    - pure XML based

```
<feed xmlns="http://www.w3.org/2005/Atom">

    <title>Example Feed</title>
    <subtitle>A subtitle.</subtitle>
    <link href="http://example.org/feed/" rel="self" />
    <link href="http://example.org/" />
    <id>urn:uuid:60a76c80-d399-11d9-b91C-0003939e0af6</id>
    <updated>2003-12-13T18:30:02Z</updated>
    
    <entry>
        <title>Atom-Powered Robots Run Amok</title>
        <link href="http://example.org/2003/12/13/atom03" />
        <link rel="alternate" type="text/html" href="http://example.org/2003/12/13/atom03.html"/>
        <link rel="edit" href="http://example.org/2003/12/13/atom03/edit"/>
        <id>urn:uuid:1225c695-cfb8-4ebb-aaaa-80da344efa6a</id>
        <updated>2003-12-13T18:30:02Z</updated>
        <summary>Some text.</summary>
        <content type="xhtml">
            <div xmlns="http://www.w3.org/1999/xhtml">
                <p>This is the entry content.</p>
            </div>
        </content>
        <author>
            <name>John Doe</name>
            <email>johndoe@example.com</email>
        </author>
    </entry>

</feed>

```