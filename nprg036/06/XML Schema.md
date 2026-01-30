# XML Schema (XSD)
XML Schema definition (XSD) is used to specify the required structure of XML documents - to specify XML formats.
W3C Recommendations
- Structures: https://www.w3.org/TR/xmlschema11-1/
- Data types: https://www.w3.org/TR/xmlschema11-2/
Currently XML Schema 1.1, 2012
as with XML 1.0/1.1, lots of parsers and validators still only support XML Schema 1.0

In this example, a structure for representation of an address is specified.

## Example
Schema:
```
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema"
           xmlns:vc="http://www.w3.org/2007/XMLSchema-versioning"
           elementFormDefault="qualified" attributeFormDefault="unqualified"
           vc:minVersion="1.1">
    <xs:complexType name="TypeAddress">
        <!-- specification of content -->
        <xs:sequence>
            <xs:element name="Street" type="xs:string"/>
            <xs:element name="Number" type="xs:integer"/>
            <xs:element name="City" type="xs:string"/>
        </xs:sequence>
        <!-- specification of attributes -->
        <xs:attribute name="Country" type="xs:string" default="CZ"/>
    </xs:complexType>
    <xs:element name="Address" type="TypeAddress"/>
</xs:schema>

```
### Documents and instances

```
<?xml version="1.0" encoding="utf-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
  ... <!-- XML schema definition  --> …
</xs:schema>
```

```
<?xml version="1.0" encoding="utf-8"?>
<root_element_of_XML_document
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="schema2.xsd">
  ... <!-- XML document --> …
</root_element_of_XML_document>
```


## Document validity
XML document is valid iff it validates against an XML schema

## Simple types
https://www.w3.org/TR/xmlschema11-2/
- boolean
- anyURI
- date, time, dateTime, dateTimeStamp
- decimal, integer, double
- hexBinary, base64Binary
- gYear


## Basic principles
Definition of
- Data types
    - Simple (simpleType)
    - Complex (complexType)
- Elements (element)
    - Groups of elements (group)
- Attributes (attribute)
    - Groups of attributes (attributeGroup)


## Element definition
Schema:
```
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:element name="Catalog"/>
</xs:schema>
```
Instance:
```
<?xml version="1.0" encoding="UTF-8"?>
<Catalog 
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:noNamespaceSchemaLocation="Schema01.xsd">
        <Dataset>
            <test/>
        </Dataset>
    </Catalog>
```

## Content type
### SimpleType
If no subelements of attributes
- restriction
- list
- union
- enumeration

Now we specified the element type to be boolean, which is a simple type.
-> the element cannot be empty, and it cannot contain other elements
-> The only permitted contents are “true” and “false”.

```
<xs:element name="Catalog" type="xs:boolean"/>
```
#### Restriction

```
<xs:element name="Catalog">
  <xs:simpleType>
      <xs:restriction base="xs:integer">
          <xs:minInclusive value="42"/>
      </xs:restriction>
  </xs:simpleType>
</xs:element>

```

#### Named type definition
We can define the new type globally in the schema and name it.
We can then use the type name to define elements.
This allows us to reuse the type definition.

```
  <xs:simpleType name="atLeast42">
      <xs:restriction base="xs:integer">
          <xs:minInclusive value="42"/>
      </xs:restriction>
  </xs:simpleType>
  <xs:element name="Catalog" type="atLeast42"/>
```
#### List

#### Type Union

#### Enumeration

### ComplexType
#### Simple content
- text content
- attributes
- no subelements


#### Complex content 
- subelements
- attributes

### Sequence
Now we specify that the Catalog element needs to have at least one (minOccurs, maxOccurs) Dataset element child.

```
<xs:complexType>
  <xs:sequence>
    <xs:element 
      name="Dataset" 
      minOccurs="1"
      maxOccurs="unbounded"/>
  </xs:sequence>
</xs:complexType>

```

#### Sequence and order
We can make the sequence itself repeat.
```
<xs:sequence maxOccurs="unbounded">
```
It is usual then to create an element representing the list of elements of the same type - Datasets, DataServices
It is then a bit clearer when there are, for instance, no DataServices

#### Choice
Alternatively to sequence, we can define a choice among alternatives

```
<xs:element name="Catalog">
    <xs:complexType>
      <xs:choice>
        <xs:element name="Dataset"/>
        <xs:element name="DataService"/>
      </xs:choice>
    </xs:complexType>
  </xs:element>
```

#### All
all is an unordered sequence - arbitrary order of elements
```
<xs:element name="Catalog">
  <xs:complexType>
    <xs:all>
      <xs:element name="Dataset"/>
      <xs:element name="DataService"/>
    </xs:all>
  </xs:complexType>
</xs:element>
```

## Reference
Element definition can reference already defined global element
- ref keyword

```
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema">
  <xs:element name="Dataset">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="name"/>
        <xs:element name="description"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
  <xs:element name="Catalog">
    <xs:complexType>
      <xs:sequence>
        <xs:element ref="Dataset"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

## Namespaces
```
<xs:schema 
xmlns:xs="http://www.w3.org/2001/XMLSchema"
targetNamespace="http://tempuri.org/" 
elementFormDefault="qualified">
  <xs:element name="Add">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="intA" 
                    type="xs:int"/>
        <xs:element name="intB" 
                    type="xs:int"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```

- targetNamespace on the schema specifies the targeted namespace.
In the instance in schema location we specify
- the namespace
- the location of the schema targeting it.
We also need to define the namespace (n1) to be able to use it in element names (n1:intA).

- elementFormDefault=”qualified” says that by default, element names must be QNames (qualified names) - use namespace prefix.
Here, it is specified on schema level and inherited to all definitions.

```
<xs:schema 
xmlns:xs="http://www.w3.org/2001/XMLSchema"
targetNamespace="http://tempuri.org/">

  <xs:element name="Add">
    <xs:complexType>
      <xs:sequence>
        <xs:element name="intA" type="xs:int"
                    form="unqualified"/>
        <xs:element name="intB" type="xs:int"
                    form="qualified"/>
      </xs:sequence>
    </xs:complexType>
  </xs:element>
</xs:schema>
```


- element form=”unqualified” says that the elements do not belong to any namespace


