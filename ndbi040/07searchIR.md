| [Previous chapter](./06graph.md.md) | [Overview](README.md) | [Next chapter](./08multimodel.md) |
| - | - | - |


# Search and Information Retrieval Systems

## Search Engines
Designed specifically for retrieval-oriented workloads.
* **Core features:** Relevance-based search, full-text search, synonym and fuzzy search.
* **Compared to Relational DBMSs:**
    * No rigid structural requirements.
    * Data may be structured, semi-structured, or unstructured.
    * Limited emphasis on relations, constraints, joins, and ACID transactions.
* **Compared to NoSQL DBMSs:**
    * Optimized primarily for searching and ranking, not editing.
    * Supports stemming, grouping, filtering, geospatial search, and analytics.
* **Architecture:** Typically built for large-scale distributed processing.
* **Optimization Goal:** Text processing, ranking, fast filtering over large collections, and distributed execution.

## Typical Use Cases
* **Full-text document retrieval:** Articles, reports, manuals, emails.
* **Product and website search:** Keyword search, faceted filtering, autocomplete.
* **Observability and log analytics:** Machine logs, traces, operational events.
* **Security and monitoring:** Anomaly investigation, incident search.
* **Analytical exploration over text-rich data:** Dashboards, aggregations, trends.

---
# Information Retrieval (IR)
A discipline focused on searching for information in large collections of documents.
* **Basic objects:** Documents, terms, and queries.
* **The central problem:** Relevance (Which documents should be returned? In what order?).
* **Challenges:** Unlike classical database querying (which relies on exact matches), IR must deal with ambiguity, synonymy, and morphology (word forms).

## Core Tasks of IR
1. **Document representation:** How text is stored and indexed.
2. **Query processing:** How a user query is interpreted.
3. **Matching:** Which documents satisfy the query.
4. **Ranking:** Which matching documents are the most relevant.
5. **Result presentation.**

## Search Engine Pipeline
1. **Data ingestion:** Documents arrive from files, databases, logs, or streams.
2. **Text analysis:** Tokenization, normalization, stemming/lemmatization, stop-word removal.
3. **Index construction:** Creation of the inverted index.
4. **Query execution:** Matching query terms against the index.
5. **Ranking and presentation:** Scoring, sorting, filtering, and aggregating results.

## The Inverted Index
* **The Problem (Why not scan all documents?):** Brute-force searching checks every document for every query. With millions of documents, this takes seconds or minutes per query.
* **The Solution:** Build an inverted index.
* **Core Idea:** Instead of mapping `Document → Words`, an inverted index maps `Term → Documents containing the term`.
* **Advantages:** Allows for extremely fast lookup of terms. Supports keyword queries, phrase queries, and boolean queries.
* **Trade-offs:** Extra storage overhead. Updates are expensive because the entire document usually must be re-indexed (no in-place updates).

---

# Elasticsearch
A distributed search and analytics engine built on top of Apache Lucene.
* **Input sources:** Application/device logs, events, monitoring data, plain text, JSON, YAML, CSV, streams.
* **Data Model:** Internally stores data as JSON documents. Data is parsed, transformed, and enriched.
* **API:** Provides a REST/HTTP API.
* **Terminology:**
    * **Document:** Basic unit of storage and retrieval (like a row).
    * **Field:** Named attribute in a document (like a column).
    * **Index:** Collection of related documents (like a table). *Note: This is different from a traditional database index.*

## Cluster Architecture
* **Nodes & Cluster:** A cluster consists of one or more server nodes.
* **Shards:** Each index can be split into shards (independent Lucene indexes) to allow for horizontal scaling and parallel query processing.
* **Replicas:** Each shard may have replicas for fault tolerance and parallel read operations.
* **Routing:** Rebalancing and routing are handled automatically. Each node can act as a coordinator to delegate operations to the respective shards. Writes go to primary shards; reads can be served by primaries or replicas.

## Query DSL (Domain-Specific Language)
* A JSON-style syntax used to execute search queries in Elasticsearch.
* **Supports:** Matching, filtering, sorting, pagination, and field selection.

## Search vs. Database Querying (Summary)
* **Elasticsearch is optimized for:** Retrieval, ranking, filtering, and aggregations over massive text collections.
* **Traditional DBMSs are optimized for:** ACID transactions, complex joins, strong consistency, and normalized in-place updates.

---

# Apache Lucene & The Elastic Stack

## Apache Lucene
* The core search library used under the hood by Elasticsearch (and Solr).
* Provides the low-level indexing and ranking capabilities: inverted indexes, ranked searching, phrase/wildcard/proximity queries, sorting, and grouping.
* **Key takeaway:** Lucene is the *search core*; Elasticsearch is the *distributed system* built on top of it.

## The Elastic Stack (Formerly ELK Stack)
Turns raw data into searchable insights and visual dashboards.
* **Beats:** Open-source data shippers installed as agents on servers to send operational data (e.g., Filebeat for logs, Metricbeat for metrics).
* **Logstash:** Parses, filters, and enriches incoming data before sending it to the database. Supports many input/output plugins.
* **Elasticsearch:** The distributed search and analytics engine.
* **Kibana:** The visualization and exploration tool (dashboards, charts, log exploration, interactive querying).

| [Previous chapter](./06graph.md.md) | [Overview](README.md) | [Next chapter](./08multimodel.md) |
| - | - | - |
