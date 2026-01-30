# XSL Transformations (XSLT)
- XSL Transformations (XSLT) Version 1.0 
    - W3C Recommendation, 1999
    - what we will cover mostly
- XSL Transformations (XSLT) Version 2.0
    - W3C Recommendation, 2007
    - most widely implemented
- XSL Transformations (XSLT) Version 3.0
    - W3C Recommendation, 2017

Tranformation to HTML

## Principles
Input 
- one or more XML document

Output
- one or more text files
- XML, HTML
- RDF Turtle
- TXT

XSLT stylesheet
- is an XML document
- stylesheet root element
- set of templates

XSLT template
- matches part of input XML document using XPath expressions
- produces output text

XSLT processor
- goes through an input XML document
- tries to match templates

## Example

```
<?xml version="1.0" encoding="UTF-8"?>
<xsl:stylesheet version="2.0" 
    xmlns:xsl="http://www.w3.org/1999/XSL/Transform"
    xmlns:xs="http://www.w3.org/2001/XMLSchema"
    xmlns:fn="http://www.w3.org/2005/xpath-functions">

    <xsl:output method="html" encoding="UTF-8" indent="yes" />
    <xsl:template match="catalog">
      <html>
        <head>
            <title>
                <xsl:value-of select="title[@xml:lang='en']"/>
            </title>
        </head>
        <body>
            <h1>
                <xsl:value-of select="title[@xml:lang='en']"/>
            </h1>
        </body>
      </html>
    </xsl:template>

    <xsl:template match="dataset">
        <h2>
            <xsl:value-of select="title[@xml:lang='en']"/>
        </h2>
        <p>
            Number of distributions:
            <xsl:value-of select="count(descendant::distribution)"/>
        </p>
    </xsl:template>

    
</xsl:stylesheet>

```

*version* attribute - version of XSLT used


*xsl:output* - specifies the output behavior of the XSLT processor
- method
    - html, xhtml, xml - produces well-formed documents
    - text - pure text output
- indent
    - yes - generates correct indentation for xml, html
    - no - only explicitly generated whitespace included in output

*match* - contains XPath expression which needs to match

*xsl:template*
- content goes to the output
    - here, we generate the HTML stub
- xsl: elements get processed
e.g xsl:value-of
- select attribute contains XPath expression
- result of the expression replaces the xsl:value-of element in the output


### Apply templates
Can be selected specific one
```
<xsl:apply-templates select="datasets/dataset"/>

```

### Named templates and parameters
Named templates
- name attribute instead of match attribute
- accept parameters
    - xsl:param - definition in named template
    - $variable - access to variable value in XPath
    - {$variable} - access to variable value elsewhere
- called using xsl:call-template
    - does not change the currently processed node set
    - xsl:with-param - values passed when calling

*xsl:element*
- creates an element on the output
- name can be constant or {$variable}


### Global variable
defined in the xsl:stylesheet root element using xsl:variable
accessible in the whole stylesheet
e.g. $lang

### Mode
ability to process the same nodes in different ways
- different templates with the same match
specified in xsl:apply-templates
used in unnamed xsl:template
- #all matches all modes


## XSLT 1.0 features
"Switch"

For each

Include - XML-based inclusion

Import - templates in importing stylesheet take precedence over imported templates

## XSLT 2.0

Grouping of data
Multiple output documents
Regular expressions

## XSLT 3.0
Streaming

Higher-order functions

Text processing: CSV, JSON, … on input

## Examples
 IANA registry - generating HTML