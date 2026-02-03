# Relational data formats

## Relational data model
- table - name, columns, rows
- primary key
- foreign key

## SQL dump
- a typical SQL dump first drops any pre-existing database and tables
- then creates new tables
- then loads data

```
DROP DATABASE IF EXISTS employees;
CREATE DATABASE IF NOT EXISTS employees;
USE employees;

DROP TABLE IF EXISTS dept_emp,
                     dept_manager,
                     titles,
                     salaries, 
                     employees, 
                     departments;

CREATE TABLE employees (
    emp_no      INT             NOT NULL,
    birth_date  DATE            NOT NULL,
    first_name  VARCHAR(14)     NOT NULL,
    last_name   VARCHAR(16)     NOT NULL,
    gender      ENUM ('M','F')  NOT NULL,    
    hire_date   DATE            NOT NULL,
    PRIMARY KEY (emp_no)
);

INSERT INTO `employees` VALUES (10001,'1953-09-02','Georgi','Facello','M','1986-06-26'),
(10002,'1964-06-02','Bezalel','Simmel','F','1985-11-21'),
(10003,'1959-12-03','Parto','Bamford','M','1986-08-28'),
(10004,'1954-05-01','Chirstian','Koblick','M','1986-12-01'),
(10005,'1955-01-21','Kyoichi','Maliniak','M','1989-09-12'),
(10006,'1953-04-20','Anneke','Preusig','F','1989-06-02'),
(10007,'1957-05-23','Tzvetan','Zielinski','F','1989-02-10'),
...
```


## DSV (Delimiter-Separated Values)
Most generic, delimiter not specified, may be anything
- Comes from the UNIX world
- logs, easy processing/cutting
- Name does not make sense
- should be Separator-Separated Values

Terminology detour:
- delimited: delimiter marks start and end of something - "id" <id>1234</id>
- separated: separator separates two things - id,departure_from,departure_at
- both delimited and separated: "id","departure_from","departure_at"

### Example
List of Czech company IDs (IČO)

- Encoding: ISO 8859-2
- Format UNL - pipe | separated
    - no specification exists, I Googled
    - probably comes from IBM Informix DB “UNLOAD” statement

```
32344|COOP družstvo Velké Meziříčí|21.02.1957||
7358|Výstavba ostravsko-karvinských dolů, a.s.|15.02.1993||
```

## TSV (Tab-Separated Values)
Tab-separated values, media (MIME) type text/tab-separated-values
Definition:
- records (rows) separated by newlines
- fields (columns) separated by tabs
- no tabs in values
- header present
- constant number of tabs per line

```
Name    Age Address
Paul    23  1115 W Franklin
Bessy the Cow   5   Big Farm Way
Zeke    45  W Main St
```

## CSV (Comma-Separated Values)
RFC 4180
media type: text/csv
Text format
- Default encoding: US-ASCII
- default changed to UTF-8 by RFC 7111 (2014)
- other encodings possible, not recommended
- Line ending: CRLF
- Column separator: , (comma)
- Escape character: "
- Escaped escape character: ""
- Optional header on first row

```
id,departure_from,departure_at,aircraft_type
24,PRG,2021-02-10T08:31:26+01:00,A380
38,DXB,2021-02-10T01:11:16+04:00,A380
72,LHR,2021-02-12T00:00:01+00:00,B747
121,AKL,2021-01-15T23:50:00+12:00,B787
```

!!! Values in CSV can contain newlines !!! => rows != records


### Excel and CSV
Microsoft Excel does not open CSV files correctly - by default
-> needs to set the loading correctly

Saving: 
To save a CSV file from MS Excel correctly, i.e.
- in UTF-8 without BOM
- separated by commas
- correctly escaped


### CSV and LibreOffice
does not auto-detect, but at least asks before opening, not only on import

### Google sheets and CSV
auto-detects correctly

### Best practices

#### Data types
Data types based on XML Schema (XSD), e.g.
xsd:boolean
✔ true, false
❌ ANO, yes, 1

xsd:integer
✔ 1, 2, 3, 4, -1, -2, 0, 2000000
❌ 1-, 2-, "2 000 000"

xsd:decimal
✔ 1.1, 1.8, -94.4
❌ 1,4, 20,4

xsd:date
✔ 2021-02-15
❌9.4.2017

xsd:time
✔09:00:00, i.e. HH:MM:SS
❌ 04:20, 4:56, 24

xsd:dateTime
✔ YYYY-MM-DDTHH:MM:SS
i.e xsd:date + "T" + xsd:time


-> rfc4180


#### Header
CSVs with missing headers are not recommended
without header, the data is even less interpretable

#### Missing values (null)
null value means the value is missing. Representing this using null is not a good idea - what does it mean?
better idea is to anticipate the reasons and specifying them explicitly. Value not recorded, equipment failure, value confidential, value not known, ...

#### Units
Use standardized units in explicit columns
http://www.unece.org/fileadmin/DAM/cefact/recommendations/rec20/rec20_Rev9e_2014.xls

#### 1NF
Cells !contain lists of values

#### No print formatting
This nicely formatted spreadsheet cannot be simply downloaded as CSV
Resulting CSV from a nicely formatted spreadsheet - it is useless

#### No sums
Sum rows or columns are for print, for humans, who do not sum easily.
They do not adhere to the schema of the table, to the column data types

#### Styles
One big CSV
- redundant
- some prefer it
- for machine learning
- excel-style filtering

Multiple CSVs
- set of normalized CSVs for loading to relational DBs
- saving space
- avoid redundancy

#### CSV publication on the Web
HTTP Content-Type header
- Content-Type: text/csv;charset=utf-8;header=present
    - For CSV files with header row
- Content-Type: text/csv;charset=utf-8;header=absent
    - For CSV files without header row


### URLs
We are able to identify a CSV file as a whole.
But how to identify a row, a column, a cell or a selection?

RFC 7111 - URI Fragment Identifiers for the text/csv Media Type (2014)

- URI fragments identifying parts of a CSV file
- rows
    - http://example.com/data.csv#row=4
- columns
    - http://example.com/data.csv#col=2
- cells
    - http://example.com/data.csv#cell=4,1
- selection
    - http://example.com/data.csv#row=3-5
    - http://example.com/data.csv#row=5-*
    - http://example.com/data.csv#col=1-2
    - http://example.com/data.csv#cell=4,1-6,2
- multi-selection (semi-colon separator)
    - http://example.com/data.csv#row=3;6


#### Fallback behavior
If the client does not know RFC 7111
URI fragments are ignored
http://example.com/data.csv#col=1-2


Results in URL of the whole file
http://example.com/data.csv


## CSV on the Web (CSVW)
A primer and a set of 4 W3C Recommendations (2015)
- Model for Tabular Data and Metadata on the Web
- Metadata Vocabulary for Tabular Data
- Generating JSON from Tabular Data on the Web
- Generating RDF from Tabular Data on the Web

Principle: Annotation of CSV tables using an additional JSON-LD descriptor.  
Use cases: Annotation, Validation, Transformation to different formats  

### Annotated tabular data model
main entities
- table group
- table
- row
- column
- cell  
Properties
- name
- titles
- schema
- ...

### "new" Types
Added aliases:
- any ~ xsd:anyAtomicType
- binary ~ xsd:base64Binary
- datetime ~ xsd:dateTime
- number ~ xsd:double

### JSON-LD Descriptor
Top-level properties within JSON-LD @context
@base - base URL (for metadata, not data)
@language - default language

```
{
    "@context": [
        "http://www.w3.org/ns/csvw",
        {
            "@language": "en",
            "@base": "https://example.org/"
        }
    ]
}
```

#### Table group
Table group with two tables  
- tables is a required property for table group

```
{
    "@context": "http://www.w3.org/ns/csvw",
    "@type": "TableGroup",
    "@id": "https://example.org/tableGroup",
    "tables": [
        {
            "url": "https://example.org/table1.csv"
        },
        {
            "url": "https://example.org/table2.csv"
        }
    ]
}

```

#### Table
url is a required property for Table
the rest are annotations using common properties
```
Standalone annotated table, i.e. not within table group
{
    "@context": "http://www.w3.org/ns/csvw",
    "@type": "Table",
    "@id": "https://example.org/table1",
    "url": "https://example.org/table1.csv",
    "dc:title": "Airports",
    "dcat:keyword": [
        "airport",
        "name",
        "airplane"
    ],
    "dc:modified": {
        "@value": "2010-12-31",
        "@type": "xsd:date"
    }
}
```

#### Table schema
- describes columns, rows and cells


#### Cell value datatypes
Added aliases:
- any ~ xsd:anyAtomicType
- binary ~ xsd:base64Binary
- datetime ~ xsd:dateTime
- number ~ xsd:double


Added datatypes: xml, html, json



#### Default values

Empty string value usually means null. However...
default
specifies string value to be used when cell contains empty string


#### Formatted numbers
xsd:double and xsd:integer should be used to represent numbers. However...
groupChar
specifies character separating groups of digits
decimalChar
specifies character serving as a decimal point

#### Formatted dates
xsd:date, xsd:time and xsd:dateTime should be used for dates and times. However...
format
for date/time datetypes specifies the date/time format


The following date/time format patterns must be recognized by implementations:

Implementations must also recognise date, time, and date/time format patterns that end with timezone markers consisting of between one and three x or X characters, possibly after a single space. These must be interpreted as follows:


### Generating RDF

Default

with no metadata other than the header row, the CSV to RDF conversion produces a simple representation of tabular metadata in RDF


Custom
ns annotated by additional properties
aboutUrl
URI template for RDF statement subject
propertyUrl
URI template for RDF statement predicate
valueUrl
URI template for RDF statement object


- notes



### Rest

#### Transformations

#### Validation


### Alternative
frictionlessdata.io - Table Schema

#### Anoated tabular data