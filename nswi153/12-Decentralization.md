
## WebSocket

- An extension of HTTP(S) that enables **two-way, real-time communication**.
- Provides **persistent** connections between client and server.
- Built on **TCP** (or **TLS/SSL** for secure connections).
- Defined in **RFC 6455**.
- Uses a **handshake** compatible with HTTP to establish the connection.
- Once established, communication is **message-based** and does not require repeated handshakes.

Use cases:
- Live chats
- Multiplayer games
- Real-time dashboards
- Collaborative applications

---

## Data and Decentralization

### InterPlanetary File System (IPFS)

- A **distributed system** for storing and accessing files, websites, and applications.
- Focused on **peer-to-peer** sharing.
- Introduced in **2015**, presented in a **Stanford seminar in 2016**.
- Files are split into **chunks**, each **cryptographically hashed**.
- Each file is assigned a **Content Identifier (CID)** based on its content.
  - When a file changes, its CID changes as well.

Advantages:
- Decentralized storage
- Immutable file versions
- Content-addressable (not location-based)

---

### Solid (SOcial LInked Data)

- An initiative led by **Tim Berners-Lee**.
- Aims to give users control over their data through **personal data pods**.
- Based on **Linked Data principles** and **Semantic Web** standards.
- Decouples apps from data — users can choose where their data lives and who accesses it.

---

### Semantic Web

- An extension of the web through **W3C standards** (e.g., RDF, OWL).
- Goal: Make **internet data machine-readable** and interoperable.
- Key technologies:
  - **RDF (Resource Description Framework)**: Describes relationships between data using triples.
  - **SPARQL**: A query language for RDF.
  - **OWL**: Web Ontology Language for rich data modeling.
  - **Schema.org**: Provides schemas for structured data (used in SEO and rich results).
    - Can be embedded using:
      - **Microdata**
      - **RDFa**
      - **JSON-LD** (preferred by Google)

---

### Decentralization Concepts

- Moving away from **centralized platforms** and ownership.
- Emphasizes:
  - **User autonomy**
  - **Open protocols**
  - **Transparency**
- Technologies:
  - **SOLID** – Data ownership and control
  - **Web 3.0** – User-centric, decentralized internet
  - **OpenPGP** – Decentralized encryption (web of trust)
  - **RDF** – Structured, linked data
  - **Blockchain** – Immutable and verifiable data storage

---

### DApp (Decentralized Application)

- Applications that run on **blockchains** or **peer-to-peer networks**.
- Frontend often similar to regular apps (HTML/CSS/JS), but backend logic is decentralized.

#### Use Cases
- **Cryptocurrencies**: Custom coins, flash loans, stablecoins
- **NFTs**:
  - Uniqueness and scarcity enforced by blockchain
  - Media often stored on **IPFS**
  - NFTs are often dropped like IPOs (Initial Public Offerings)
- **Gaming**:
  - Players can **earn assets** and **transfer them across games**
  - Enables true ownership of in-game items

#### Benefits
- **Decentralization**: No single authority
- **Censorship resistance**: Immutable data
- **Transparency**: Public, verifiable data
- **Trust**: Code and data are visible and auditable

> "One bad actor can’t change your balance — trust is distributed."

---
