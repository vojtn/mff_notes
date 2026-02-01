# Common RDF vocabularies
both machine and human readable documents  
describes what IRI means and what are defined  
Catalog of vocabularies used on the Web of Data
-> Basic rule - vocabulary reuse

RDF Vocabulary = collection of classes and properties, their IRIs and their definitions

# Dublin core (dcterms)
Standardization of naming organization.  
Otherwise people would call same things differently like name/title/label  
Origin - librarians community for standardization of books properties (1995: OCLC/NCSA Metadata Workshop)

## Properties
- contributor
- coverage
- create
- creator
- date
- description
- format
- identifier
- language
- publisher
- relation
- rights
- source
- subject
- title
- type

2 namespaces:
1. dc (http://purl.org/dc/elements/1.1/)
    - original one
    - dc: prefix
    - depricated for our purpose
2. dcterms (http://purl.org/dc/terms/)
    - The one we use
    - dcterms: prefix


## Example (dcterms:publisher)
```
Term Name: publisher
More details
    URI: http://purl.org/dc/terms/publisher
    Label: Publisher
    Definition: An entity responsible for making the resource available.
    Type of Term: Property
    Range Includes: http://purl.org/dc/terms/Agent
    Subproperty of: Publisher (http://purl.org/dc/elements/1.1/publisher)
```

## Example 
```
ex:catalog a dcat:Catalog;
ex:catalog dcterms:title "my catalog"
ex:catalof dcterms:decription "my first testing catalog"
```

# SKOS (Simple Knowledge Organization System)
For codelists and taxonomies   
e.g. grades in students information systems.

- W3C recommendation
- August 2009
- for hierarchies and collections of concepts 


## skos:Concept
Represent idea, notion or unit of thought

Sights and landmark from tripadvisor
```
<https://example.org/resource/attraction-types/sights-and-landmarks> a skos:Concept .
```

## skos:ConceptScheme
Codelist or group of concepts

- Aggregation of one or more concepts
- Semantic relations between the concepts
- Roughly corresponds to
    - Individual thesaurus
    - Classification scheme
    - Subject heading system

```
<https://example.org/resource/attraction-types> a skos:ConceptScheme ;
    skos:hasTopConcept <https://example.org/resource/attraction-types/sights-and-landmarks> .

<https://example.org/resource/attraction-types/sights-and-landmarks> a skos:Concept ;
    skos:inScheme <https://example.org/resource/attraction-types> ;
    skos:topConceptOf <https://example.org/resource/attraction-types> .

```
Multiple level possible
- hasTopConcept -> points to the top concept
- topConceptOf


## Labels
We need human readable label to the resources and object

### skos::prefLabel
- published choosen
- label in natural language - has language tags
- for every language there is one prefferend label

### skos::altLabel
- not prefered
- multiple per language
- cannot be the same as prefLabel

### skos:hiddenLabel
- usage for common misspelings
- easier to search them but user cant see them 

```
<MyConcept> 
  skos:prefLabel "animals"@en ; 
  skos:altLabel "fauna"@en ; 
  skos:hiddenLabel "aminals"@en ; 
  skos:prefLabel "animaux"@fr ; 
  skos:altLabel "faune"@fr .
```

### skos:notation
- intended to be machine readable not human
- example with the students information system
- does not have a language tag
- can have a custom data type

```
<MyConcept> skos:notation "303.4833"^^<MyNotationDatatype> .
```

## Example

```
@prefix atold: <http://publications.europa.eu/resource/authority/> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix skos: <http://www.w3.org/2004/02/skos/core#> .

<http://publications.europa.eu/resource/authority/continent/AFRICA> a skos:Concept ;
    skos:inScheme atold:continent ;
    skos:prefLabel "Африка"@bg ,
        "Africa"@cs,
        ...
        "Africa"@en .

<http://publications.europa.eu/resource/authority/continent/AMERICA> a skos:Concept ;
    skos:inScheme atold:continent ;
    skos:prefLabel "Америка"@bg,
        "Amerika"@cs,
        ...
        "America"@en .
```

## skos:semanticRelation
Semantic relations between concepts within the same concept scheme.

- skos:related
- skos:broaderTransitive
    - skos:broader
- skos:narrowerTransitive
    - skos:narrower

## Collections
Useful if some concepts share something in common and/or can be meaningfully ordered.

### skos:Collection
skos:member

### skos:OrderedCollection
skos:memberList

```
<MyCollection> a skos:Collection ; 
  skos:member <A> , <B> , <MyNestedCollection> .

<MyNestedCollection> a skos:Collection ;
  skos:member <X> , <Y> , <Z> .

<MyOrderedCollection> a skos:OrderedCollection ;
  skos:memberList ( <X> <Y> <Z> ) .
```

## Mappings 
To specify mapping/alignment between different concept schemes.

skos:mappingRelation

## skos:exactMatch 
- means that a concept from another conceptScheme means exactly the same
- concepts can be used interchangeably
- transitive (A exactMatch B . and B exactMatch C . -> A exactMatch C .)

## skos:closeMatch
- is not transitive
- similar concepts, but not fully interchangeable (almost same)

## skos:broadMatch
- The external concept is broader than the local one
-> A is more specific than B
```
ex:HeartAttack skos:broadMatch ex:CardiovascularDisease .
```

## skos:narrowMatch
- reverse of broadMatch
-> B is more specific than A
```
ex:Vehicle skos:narrowMatch ex:ElectricCar .
```

## skos:relatedMatch
- weakest association

```
<https://data.mvcr.gov.cz/zdroj/číselníky/pohlaví/položky/ženské> a skos:Concept;
  skos:inScheme <https://data.mvcr.gov.cz/zdroj/číselníky/pohlaví>;
  skos:prefLabel "Female"@en, "Ženské"@cs ;
  skos:exactMatch <https://data.cssz.cz/resource/ciselniky/ciselnik-pohlavi/2/2009-01-01>,
                  <http://publications.europa.eu/resource/authority/human-sex/FEMALE> .
```

# GoodRelations (gr)
The Web Vocabulary for E-Commerce
- Author: Martin Hepp
- Used by Google, Yahoo, BestBuy, sears.com, kmart.com and 10 000 more...
- Syntax-neutral: Microdata, RDFa, RDF/XML, Turtle, JSON, OData, GData, …
- Industry-neutral: consumer electronics, cars, tickets, real-estate, ...
Different stages of the value chain
raw materials, after-sales services

## gr:BusinessEntity
person or organization

```
foo:ACME a gr:BusinessEntity;
    gr:legalName "ACME Bagel Bakery Ltd."@en;
    foaf:page <http://www.example.com/>;
    s:address [ a s:PostalAddress;
                s:streetAddress "Bagel Street 1234";
                s:postalCode "12345";
                s:addressLocality "Munich, Germany" ];
    s:telephone "+49-89-12345678-0";
    s:faxNumber "+49-89-12345678-99";
    s:email "contact@example.org".
```

## gr:ProductOrService
camcorder, house, car
haircut

## gr:Offering
To transfer some rights (ownership, usage, license) on the object or
To provide the service for a certain compensation (money)  
Made by the agent and related to the object or service

## gr:Location
From which this offer is available
store, bus stop, gas station

```
foo:pos a gr:Location;
    gr:name "Hepp's Bagel Restaurant Munich - Bagel Street"@en;
    s:address [ a s:PostalAddress;
                s:streetAddress "Bagel Street 1234";
                s:postalCode "12345";
                s:addressLocality "Munich, Germany" ];  
    s:geo [ a s:GeoCoordinates ;
            s:latitude 45.75;
            s:longitude 49.98 ];
    s:telephone "+49-89-12345678-0" .
```

## gr:OpeningHoursSpecification
One gr:OpeningHoursSpecification entity specifies a time interval, and links to days
Typically, full specification contains multiple entities

```
foo:restaurant a gr:Location;
    gr:name "Hepp's Happy Burger Restaurant"@en;
    gr:hasOpeningHoursSpecification 
         [ a gr:OpeningHoursSpecification;
           gr:opens "08:00:00"^^xsd:time;
           gr:closes "12:00:00"^^xsd:time;
           gr:hasOpeningHoursDayOfWeek gr:Monday,
           gr:Tuesday, gr:Wednesday, gr:Thursday, 
           gr:Friday ],
         [ a gr:OpeningHoursSpecification;
           gr:opens "13:00:00"^^xsd:time;
           gr:closes "20:00:00"^^xsd:time;
           gr:hasOpeningHoursDayOfWeek 
           gr:Friday ] .
```

## gr:Offering
```
foo:offer a gr:Offering;
     gr:name "Hepp Personal SCSI Controller Card"@en;
     gr:description """The Hepp Personal SCSI is a 16-bit add-on card that allows attaching up to seven SCSI devices to your computer."""@en;
    
     gr:hasBusinessFunction gr:Sell;
     gr:condition "used";

     gr:hasEAN_UCC-13 "1234567890123"^^xsd:string;
     gr:hasMPN "PSCSI"^^xsd:string;
     gr:hasStockKeepingUnit "123-456"^^xsd:string;
     gr:hasInventoryLevel [ a gr:QuantitativeValue;
                            gr:hasMinValue "1"^^xsd:float ];

     s:aggregateRating [ a s:AggregateRating;
                         s:ratingValue "4.9"^^xsd:float;
                         s:reviewCount 99 ];

     foaf:depiction <http://example.com/images/pscsi.jpg>;
     foaf:page <http://example.com/products/pscsi> . 
```

## gr:Offering
```
foo:offer a gr:Offering;
      gr:hasPriceSpecification [ a gr:UnitPriceSpecification;
          gr:hasCurrency "USD"^^xsd:string;
          gr:hasCurrencyValue "99.99"^^xsd:float;
          gr:validThrough "2012-11-30T23:59:59"^^xsd:dateTime ];
```

## Product or service
Real product (gr:Individual)
- laptop with its serial number
- car with its VIN
- can be sold only once

Product model (gr:ProductOrServiceModel)
- NIKON T90
- Abstract definition, not a particular item

Black boxes of products (gr:SomeItems)
- Amazon page for a new book
- Multiple items of some type, can be sold more times


```
foo:myVolkswagenBeetle a <http://www.productontology.org/id/Automobile>, gr:Individual;
    gr:name "1973 Volkswagen Beetle"@en;
    gr:description """This car is simply unique - it has been owned by Madonna."""@en .

foo:model a gr:ProductOrServiceModel;
    gr:name "ACME Colorvision 123"@en;
    gr:description "The ACME Colorvision 123 is the leading-edge color TV from our company."@en;
    gr:hasEAN_UCC-13 "1234567890123"^^xsd:string;
    gr:width [ a gr:QuantitativeValue;
               gr:hasValueFloat "102.0"^^xsd:float;
               gr:hasUnitOfMeasurement "CMT"^^xsd:string ];
    gr:height [ a gr:QuantitativeValue;
               gr:hasValueFloat "60.0"^^xsd:float;
               gr:hasUnitOfMeasurement "CMT"^^xsd:string ].

foo:product a gr:SomeItems;
    gr:name "Canon Rebel T2i (EOS 550D)"@en;
    gr:description "The Rebel T2i EOS 550D is Canon's latest digital SLR camera."@en;
    gr:hasEAN_UCC-13 "9781906672799"^^xsd:string;
    foaf:depiction <http://www.example.com/canon_rebel_t2i.jpg>;
    foaf:page <http://www.example.com/canon_rebel_t2i.html> .
```

## Linking the data
```
foo:be a gr:BusinessEntity;
    gr:offers foo:offer .
foo:offer a gr:Offering .

foo:offer a gr:Offering;
    gr:includes foo:product .

foo:be a gr:BusinessEntity;
    gr:hasPOS foo:pos .
foo:pos a gr:Location .
```

## gr:QuantitativeValue
```
foo:product a gr:ProductOrServiceModel;
    gr:name "ACME Electric Anvil"@en;
    gr:weight [ a gr:QuantitativeValue;
                gr:hasUnitOfMeasurement "KGM"^^xsd:string;
                gr:hasValue "50"^^xsd:float ];
    foo:voltage [ a gr:QuantitativeValue;
                gr:hasUnitOfMeasurement "VLT"^^xsd:string;
                gr:hasMinValue "100"^^xsd:integer;
                gr:hasMaxValue "220"^^xsd:integer ].
```

Units:
- MTR(m)
- MTK(m²)
- MTQ(m³)
- KGM (kg)

## gr:QuanlitativeValue
```
foo:GarmentSize a rdfs:Class;
    rdfs:subClassOf gr:QualitativeValue;
    rdfs:label "Garment sizes (value class)"@en.
    
foo:M a foo:GarmentSize;
    rdfs:label "M - Medium."@en;
    gr:lesser foo:L.

foo:L a foo:GarmentSize;
    rdfs:label "L - Large."@en;
    gr:greater foo:M.

foo:size a rdf:Property ;
   rdfs:subPropertyOf gr:qualitativeProductOrServiceProperty ;
   rdfs:range foo:GarmentSize ;
   rdfs:label "size (0..1)"@en .
    
foo:tshirt a gr:SomeItems;
    gr:name "Blue T-Shirt (Size M)"@en;
    gr:color "blue"@en;
    foo:size foo:M.
```


# [Schema.org](www.Schema.org)
Schema.org is a collaborative, community activity with a mission to create, maintain, and promote schemas for structured data on the Internet, on web pages, in email messages, and beyond.

- Founded by Google, Microsoft, Yahoo and Yandex
- Integrates existing vocabularies, creates new terms
    - foaf, GoodRelations, DCAT ...
- Maintained on GitHub
- 817 types, 1518 properties, 521 enumeration values (2025)

## Schema.org & GoodRelations 2012 approach
Different paradigm
- allowing publishers to publish rough, low-quality data - so that they publish at least something, and quickly - leaving the integration burden on consumers
- instead of making publishers publish data of higher quality, using proper code lists, allowing the data to be consumed easily

```
<#model> a schema:Product ;
    schema:name "ACME Electric Anvil" ;
    schema:feature [ a schema:ProductFeature ;
        schema:propertyName "Power supply" ;
        schema:propertyValue "110-220" ;
        schema:unitText "Volts" ] ;
    schema:feature [ a schema:ProductFeature ;
        schema:propertyName "Weight" ;
        schema:propertyValue "2.25" ;
        schema:unitText "kg" ] ;
    schema:feature [ a schema:ProductFeature ;
        schema:propertyName "Safety belt" ;
        schema:propertyValue "yes" ] . 
```
Primary usecase:
- extraction of data from web pages
- primarily based on HTML Microdata
    - then RDFa
    - eventually JSON-LD

=> use rdf:langString (language tags) and proven XML Schema datatypes



# FOAF (Friend of a friend)
TODO: Bonus