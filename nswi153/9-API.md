# API (Application Programming Interface)
An **interface** that allows different software components or systems to **communicate** with each other.
- Defines how to request services or exchange data.
- Can be local (within a system) or remote (over a network).

--- 

## RPC (Remote Procedure Call)
Allows a program to **call functions on a remote system** as if they were local.

- Requires standardization of:
  - **Protocol** (e.g., how to send the call)
  - **Arguments and results** (serialization format)

### Formats
- **XML-RPC** – uses XML to encode remote calls.
- **JSON-RPC** – lightweight alternative using JSON.

### Modern Version
- **tRPC** – TypeScript-based framework that allows type-safe RPC in full-stack TypeScript apps. No manual API schema needed.

---

## SOAP (Simple Object Access Protocol)
A **protocol** for exchanging structured information in web services.

- XML-based, standardized, and extensible.
- More formal and feature-rich than REST.
- Supports protocols like HTTP, SMTP, etc.
- Uses **WSDL** (Web Services Description Language) to describe the API.
- Successor to XML-RPC

--- 

## REST (Representational State Transfer)

An **architectural style** for designing networked applications, defined by Roy Fielding.

Originally not specific to HTTP, but widely adopted as a model for **HTTP-based web APIs**.

### Core REST Constraints
1. **Client-Server** – separation of concerns.
2. **Stateless** – each request is independent.
3. **Cacheable** – responses must indicate cacheability.
4. **Uniform Interface** – standardized way to access resources.
5. **Layered System** – components may be layered for scalability.
6. *(Optional)* **Code on Demand** – clients can download executable code.

---

## REST vs RESTful API

| Concept         | REST (Architectural Style)          | RESTful API (Implementation)                 |
|----------------|--------------------------------------|----------------------------------------------|
| Type           | Abstract theory                      | Practical API design                          |
| Defined by     | Set of constraints                    | Follows those constraints (fully or partially)|
| Protocol       | Protocol-agnostic                     | Typically uses HTTP                           |
| Example        | Design pattern                       | GitHub API, Twitter API, etc.                 |
| Format         | Not defined                          | Often uses JSON or XML                        |

- Not all APIs claiming to be RESTful follow all constraints — they may be "REST-like".

---

## OpenAPI
OpenAPI is a **specification** for describing and documenting **RESTful APIs** in a machine-readable format.

- Defines available **endpoints**, **methods**, **parameters**, and **response formats**.
- Helps generate client libraries, server stubs, and interactive documentation.
- **Language-agnostic**.
- Uses **YAML** or **JSON** for defining the specification.
- Originally called **Swagger** — renamed to OpenAPI in **2015** after joining the Linux Foundation.

### Related Tools
- **Swagger Editor** – for writing OpenAPI specs.
- **Swagger UI** – interactive browser-based API explorer.

---

## AsyncAPI

**AsyncAPI** is a specification for documenting **event-driven** and **asynchronous APIs** (e.g., via WebSockets, MQTT, Kafka).

- Inspired by OpenAPI but for **message-based architectures**.
- Language-agnostic and open standard.
- Supports schema definitions, message formats, channels, and operations.
- Useful for documenting **publish/subscribe** systems and **streaming services**.

---

## GraphQL
A **query language** and **runtime** for APIs, originally developed by Facebook.

- Designed to solve REST’s limitations like **overfetching** (getting too much data) and **underfetching** (not getting enough).
- Allows clients to request **exactly the data they need**.
- Uses a **single endpoint** for all operations.
- **Language-agnostic** – works with many server/client platforms.
- Released in **2015** (internally used by Facebook since 2012).
- Great ecosystem 

### Key Features
- **Flexible Queries** – fetch only specific fields.
- **Strongly Typed Schema** – defines types, queries, and mutations.
- **Introspection** – the API describes itself, enabling auto-generated docs and tools like GraphiQL.

- hard to achive and keep all the positives
- caching issues 

### GraphQL Schema
Defines:
- **Types** (e.g., `User`, `Post`)
- **Queries** (read operations)
- **Mutations** (write operations)
- **Subscriptions** (real-time updates)

---

## MCP (Model-Context-Protocol)
- text description of the API (human readable)
- A proposed protocol format from **Anthropic** for interacting with **Large Language Models (LLMs)**.
- Aims to standardize the structure of messages exchanged between a user and a model.
- Helps LLMs understand the **model type**, **context** of the conversation, and **communication protocol**.
- Still in early adoption stages – used more in LLM research and experimentation.
