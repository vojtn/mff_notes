# Wikidata
Free encyclopedic database
- Like Wikipedia, but for facts, not documents
- Community-built and community-managed
- Anyone can contribute
- Anyone can edit anything
- Queryable via SPARQL endpoint

# DBpedia
Data is scraped from Wikipedia data boxes

# Data model
wikibase is the software running wikidata and other instanes
Wikidata = one of wikibase intances

## Truthy values
straightforward RDF
the one with best rank

## Item 
basic thing in Wikidata
- has item identifier - QID, Q number
- has labels, descriptions and aliases in various languages

## Statement
about Items
- Property with PID - property ID
- Value
- Qualifiers
    - property
    - value
- References
    - property
    - value
- Rank

# Query Service
Wikidata Query Service is SPARQL based, with some extensions.
Note:
- QIDs and PIDs for items and properties - not human readable
- The user interface is a bit smarter than the usual SPARQL endpoint’s, it will provide hints in tooltips
- various prefixes for usage in statements, qualifiers, references and values
- there is plenty of tutorials and examples

- offers visualizations of the resulting data