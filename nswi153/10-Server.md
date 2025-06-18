[Back to overview](/Readme.md)


# Server

## Monitoring

### OpenTelemetry (OTel)

- Introduced in **2019**.
- A **vendor-neutral observability framework** for collecting telemetry data such as:
  - **Traces**
  - **Metrics**
  - **Logs**
- Helps developers instrument code and export data to observability tools.
- **Not** a backend like:
  - **Prometheus** (metrics)
  - **Jaeger** (traces)
  - **Grafana**, **Zipkin**, etc.
- OpenTelemetry provides SDKs and APIs for many languages.

---

## Background Jobs

- Used for **asynchronous or delayed processing** outside the main request/response cycle.
- Common use cases:
  - Sending emails
  - Processing images
  - Scheduled tasks
  - Web scraping

### Message Queues

- Systems that **receive, hold, and deliver messages** between components.
- Support decoupling and scalability.
- Can be synchronous or asynchronous.

### Task Queues

- Maintain a list of background tasks to be executed.
- Often backed by message queues.

---

## Application State

- **Stateful**: Server retains information across sessions (e.g., sessions, login).
- **Stateless**: Each request is independent; no server-side session is maintained.
  - Easier to scale
  - Required for RESTful APIs

---

## Proxy

- acts on behalf of the client:
  - Client sends request → proxy → target server → proxy → client.
- **Enhancements** (via proxy plugins/modules):
  - SSL termination
  - Compression
  - Caching
  - Monitoring
  - Routing to different locations or services

Use cases:
- Serving static content
- Filtering
- Performance improvements

---

## Reverse Proxy

- acts on behalf of the server.
- Client sends requests to the reverse proxy, which forwards them to the appropriate backend service.

Benefits:
- Single point of access
- Security (hides internal services)
- Load balancing
- SSL termination
- Centralized logging
- Caching

Common tools:
- **Nginx**
- **HAProxy**
- **Traefik**
- **Apache HTTP Server**

---

## Cache

- Improves response time and reduces load on backends.
- Caching can occur at various layers:
  - Client (browser cache)
  - CDN
  - Web server
  - Application server
  - Database

### Cache Invalidation

- One of the hardest problems in computer science.
- Ensures stale data is cleared or updated when needed.

---

## Load Balancer

- Distributes incoming traffic across multiple servers to ensure:
  - High availability
  - Horizontal scaling
  - Fault tolerance

Features:
- Can be **software-based** (Nginx, HAProxy, Envoy) or **hardware appliances**.
- Supports:
  - Round-robin
  - Least connections
  - IP hash
- **Sticky sessions**: Keep users connected to the same server.

---

## Gateway

- An **API Gateway** acts as an entry point for client requests to microservices.
- Combines functionality of reverse proxy and API management.
- May include:
  - Authentication
  - Rate limiting
  - Logging
  - Protocol translation (HTTP - gRPC)
  - Request transformation

Popular tools:
- **Kong**
- **NGINX**
- **Traefik**
- **AWS API Gateway**

---

## Content Delivery Network (CDN)

- A **distributed network of servers** located across the globe.
- Delivers content from the closest edge location to the user, minimizing latency.

Use cases:
- Serving **static files** like:
  - HTML, CSS, JS
  - Images, videos
- Reduces load on origin servers and speeds up page load times.

Popular CDNs:
- **Cloudflare**
- **Amazon CloudFront**

---

[Back to overview](/Readme.md)
