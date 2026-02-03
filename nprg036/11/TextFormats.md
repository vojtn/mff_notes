# Historical text formats

## Text file, plain text
Text file stores plain text
Sequence of lines of text, no formatting
a.k.a. flat file
Line endings vary
- Windows: CR+LF
- Unix, modern macOS: LF
- Mac OS (before Mac OS X): CR

most application, operating system and architecture independent format
plain text - no clear definition, usually “no formatting”

Arbitrary encoding, traditionally US-ASCII, nowadays UTF-8 recommended
e.g. ISO-8859-2 (Latin 2) or CP1250 (Windows 1250) in Central Europe

Media type: text/plain
File extension: .txt

## Formatted text 
Underlining initially not available in text files.
Substitutes:
```
This is VERY important
This is _very_ important
This is *very* important
This is v e r y important
```

## Richtext
RFC 1341, 1992
Extremely simple, yet extensible syntax
- formatting commands between < and >
- command no more than 40 characters
- may be preceded by /, making them negations
- balanced formatting commands and negations, with 3 exceptions (<lt>, <nl>(required line break), <np>(page break))
- Extremely limited capabilities
- Compatibility with SGML
US-ASCII encoding, can be explicitly switched\
Media type: text/richtext

```
<bold>Now</bold> is the time for
<italic>all</italic> good men
<smaller>(and <lt>women>)</smaller> to
<ignoreme></ignoreme> come
          
to the aid of their
<nl>
beloved <nl><nl>country. <comment> Stupid
quote! </comment> -- the end
```

## Enriched text
RFC 1896, 1996
Evolution of Richtext
- e.g. parameters of formatting commands
- << instead of <lt>
- N+1 CRLFs => N actual line breaks
Focused on Internet mail
Parallel to HTML, Reasons:
- Not every Internet mail parser supports HTML or can easily strip it from text
- Features in HTML unnecessary for mail
US-ASCII encoding, can be explicitly switched
Media type: text/enriched

```
From: Nathaniel Borenstein <nsb@bellcore.com>
To: Ned Freed <ned@innosoft.com>
Content-type: text/enriched


<bold>Now</bold> is the time for <italic>all</italic>
good men
<smaller>(and <<women>)</smaller> to
<ignoreme>come</ignoreme>


to the aid of their

<color><param>red</param>beloved</color>
country.
```


## Rich Text Format (RTF)
Rich Text Format (RTF)
Microsoft, 1987 - 2008
- Proprietary format inspired by TeX
    - Initially unavailable specification
    - Reverse-engineering when MS updated
- Meant for saving and sharing of documents
    - by WYSIWYG editors
    - not direct editing as text
- Its own subset of character encodings
    - All 7-bit, i.e. Windows-*, e.g. Windows-1250
    - Since RTF 1.5 (1997) also UTF-16 escapes
Media type: text/rtf
File extension: .rtf

Text-based alternative to binary formats for storage of formatted text such as MS Word .doc
New RTF version with each new version of MS Word

```
{\rtf1\ansi\ansicpg1252 This is an RTF file. It supports \b bold\b0  and \i italics\i0 , and so much more.}
```

## 602
602 format by Software602, 1988
- Specific Czech text format
used in the Text602 text editor for MS-DOS
Wide-spread in Czech public administration, companies and schools in 1990s.
Uses ASCII control characters (unprintable) for formatting, e.g.
- 02 for bold
- 04 for italics
602 format can be opened by LibreOffice Writer
File extension: .602


# Modern text formats for the Web

## HTML (HyperText Markup Language)
- HTML, Tim Berners-Lee, CERN, 1991
- HTML 2.0 IETF RFC 1866, 1995
- HTML 3.2 W3C Recommendation, 1997
- HTML 4.01 W3C Recommendation, 1999
- HTML 5, W3C Recommendation, 2014
- HTML 5.2 W3C Recommendation, 2017
- HTML Living Standard, WHATWG, 2019+

Media type: text/html
File extension: .html .htm

Markup - not visible after document is presented/rendered

### XHTML
HTML elements with XML rules
- e.g. every element has to be empty or has to be closed (HTML: <br>, XHTML: <br/> or <br></br>)
- attributes must have values (HTML: <input required> </input>, XHTML: <input required=”required”> </input>)

## Markdown
John Gruber and Aaron Swartz, 2004
Markup language
- Readability of source code by humans
- Easy conversion to valid (X)HTML
“HTML is a *publishing* format; Markdown is a *writing* format”
Media type: text/markdown
File extension: .md

[Editor dillinger](https://dillinger.io/)

### Headers
Setext Style (2 levels)
```
===
---
```
atx-style (6 levels)
```
# Level 1
## Level 2
```

### Emphasis
```
**string**
__strong__
```

### Unordered lists
```
*
*

+
+

-
-
```

### Ordered lists

```
1.
2.
3.
```

### Links
Inline
```
[link](www.example.com "With a title")
```
Reference
```
I get 10 times more traffic from [Google][1] than from [Yahoo][2] or [MSN][3].

[1]: http://google.com/ "Google"
[2]: http://search.yahoo.com/ "Yahoo Search"
[3]: http://search.msn.com/  "MSN Search
```
Reference style makes the text even more readable, helps avoid duplicate links and resembles style of rendered or printed text.

### Images
```
![alt text](/path/to/img.jpg "Title")

![alt text][id]

[id]: /path/to/img.jpg "Title"
```

### Code
Inline
```
`<blink>`
```

Block
```
    <blockquote>
        <p>For example.</p>
    </blockquote>
```


### Horizontal rule

```
* * *

***

*****

- - -

----------------------------------
```

### Markdown flavours
Original 2004 Markdown 1.0.1 spec ambiguous
=> implementations diverged, many incompatible extensions

- CommonMark
- CriticMarkup
- Discount
- DocFX
- ...

### CommonMark
Markdown fans, 2014-2021 (v0.30)
-> improve standardisation
-> better testability
- standard, unambiguous syntax specification for Markdown
- suite of comprehensive tests for implementations
- set up commond superset of markdown

Implements:
- Discourse
- GitHub
- GitLab
- Reddit
- Qt
- Stack Overflow / Stack Exchange
- Swift

#### Code blocked
Allows info strings (language id)
```
~~~
```
~~~
```
~~~

#### Hard line breaks

```
foo..
again\
```

### Kramdown - tables

```
| Header1 | Header2 | Header3 |
|:--------|:-------:|--------:|
| cell1   | cell2   | cell3   |
| cell4   | cell5   | cell6   |
```

### Use cases
- GitHub/GitLab readme.md and wiki
- [Jekyll](https://jekyllrb.com/) - static site generated - used in GitHub pages

## Wikitext
Magnus Manske, Lee Daniel Crocker, 2002
- No formal specification, just implementations
    -  Quite complex, see full guide
- MediaWiki - software powering Wikipedia and 10 000s other Wiki sites
    - tens of other implementations
    - differences in Wikitext syntax

```
'MediaWiki''' is a [[Free and open-source software|free and open-source]] [[wiki software]]. It was developed for use on [[Wikipedia]] in 2002, and given the name "MediaWiki" in 2003.<ref name=MediaWiki_history/> It remains in use on Wikipedia and almost all other [[Wikimedia movement|Wikimedia]] 
```

### Headings
```
= Heading 1 =
== Heading 2 ==
=== Heading 3 ===
==== Heading 4 ====
...
```

### Text formating 
```
''italics'', '''bold''', and '''''both'''''
```

### Lists
```
* one
* two
** two point one
```

### Links
```
[[copy edit]]
[[copy edit]]ors

[[Android (operating system)|Android]]
[[Frog#Locomotion|locomotion in frogs]]
```



## TeX
Donald Knuth, 1978
Free, widely-used typesetting programming language and software
- to allow anybody to produce high-quality books with minimal effort
- to provide a system that would give exactly the same results on all computers, at any point in time
File extension: .tex
- focused on formatting, it is low-level, used by creators of macros and templates for actual documents
de facto standard for publication of texts in technical fields
- computer science
- mathematics
- engineering
- physics


## LaTeX
Leslie Lamport, 1984
Set of TeX macros
- to focus authors on writing of documents
    - their content, not their format
Letting authors format documents results in
1. lots of author time consumed by design
2. lots of badly designed documents

Supports:
- Typesetting journal articles, technical reports, books, and slide presentations
- Large documents containing sectioning, cross-references, tables and figures
- Complex mathematical formulas
- Automatic generation of bibliographies and indexes
- Multilingual typesetting


```
documentclass{article}
\usepackage{amsmath}

\begin{document}
Hello world!
\[
    \binom{n}{k} = \frac{n!}{k!(n-k)!}
\]
\end{document}
```


### Packages
LaTeX packages provide functionalities
CTAN: Comprehensive TeX Archive Network
- Currently 6500+ packages
Packages are defined in preamble
- using \usepackage[options]{package}
- after \documentclass{}
- before \begin{document}
E.g. package amsmath provides the \binom and \frac commands 

### Metadata
article class defines, how the title, author and date is typeset by \maketitle
UTF-8 encoding
```
\documentclass{article}
\usepackage[utf8]{inputenc}

\title{First document}
\author{Jakub Klímek}
\date{May 2021}

\begin{document}

\maketitle

First document. This is a simple example, with no 
extra parameters or packages included.
\end{document}
```

### Sections
```
\part{name}
\chapter{name}
\section{name}
\subsection{name}
\subsubsection{name}
\paragraph{name}
\subparagraph{name}
\section*{name}
```

### Lists
```
\begin{itemize}
    \item One
    \item Two
    \item Three
\end{itemize}

\begin{enumerate}
    \item One
    \item Two
    \item Three
\end{enumerate}
```

### Labels and references
\label{name}
- defines a label
- for the latest counter name and number, e.g.
    - counter name: section
    - counter number: 1
\autoref{name}
- in package hyperref
- references a label
- correct name as part of link
    - section
    - figure
(takes care of proper reference name and its capitalization, e.g. at the beginning of a sentence)


### Figures
```
\begin{figure}
    \centering
    \includegraphics[width=0.25\textwidth]{mesh}
    \caption{a nice plot}
    \label{fig:mesh1}
\end{figure}
```

### Bibliography
BibTex - references management tool
\cite - references an entry from a .bib file from a .tex file
.bib file - specific text format for 

```
The authors of the paper I read \cite{myPaper} say that BibTeX is cool.

\bibliographystyle{unsrt}
\bibliography{references}
```

```
@article{myPaper,
  author    = {Jakub Klímek and
               Petr Škoda and
               Martin Nečaský},
  title     = {{Survey of tools for Linked Data consumption}},
  journal   = {Semantic Web},
  volume    = {10},
  number    = {4},
  pages     = {665--720},
  year      = {2019},
  url       = {https://doi.org/10.3233/SW-180316},
  doi       = {10.3233/SW-180316}
}
```

# Usage of text

## Text search
- exact match
- wildcard search
- regular expressions

## Inverted index
- search in database of documents

## Text comparison
- diff

## Named entity recognition
DBpedia Spotlight

Results of NER can be used for better search, e.g.
“Texts where cities are mentions” - returns texts where Berlin or Potsdam is mentioned

- conversion of regular text to structured data -> detection of keywords (entit)