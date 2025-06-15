# Server

## CGI (Common Gateway Interface)

- A **standard protocol** for interfacing external applications with web servers.
- Allows dynamic content generation.
- Typically used to run scripts or programs (in Perl, Python, etc.) on the server in response to web requests.
- The **web server executes the CGI program**, passing it request data via environment variables and stdin.
- Now considered **obsolete** due to poor performance (starts a new process for every request).

---

## Web Server

- software (and underlying hardware) that handles **HTTP requests** from clients (browsers) and responds with HTML, CSS, JS, files, etc.
- Can serve **static content** or **forward requests** to an application server for dynamic content.
- Popular web servers:
  - **Apache HTTP Server**
  - **Nginx**
  - **Caddy**
  - **Microsoft IIS**
- Web servers can interface with different languages and frameworks via:
  - CGI
  - FastCGI
  - Reverse proxy
  - Modules or plugins

---

### Flask

- A **micro web framework** for Python.
- Lightweight, minimal, and flexible.
- Great for small to medium applications.
- Offers routing, templating (Jinja2), request handling.
- You can extend it with plugins (for databases, auth, etc.).

Other Python web frameworks:
- **Django** (batteries-included)
- **FastAPI** (modern async + OpenAPI support)

---

## Node.js

- A **JavaScript runtime environment** built on Chrome's V8 engine.
- Allows writing **server-side JavaScript**.
- Non-blocking, event-driven architecture.
- Commonly used for building APIs and real-time applications.

---

### Express.js

- The most popular **web framework for Node.js**.
- Minimalistic and unopinionated — gives control to developers.
- Features:
  - Middleware support
  - Routing
  - HTTP utility methods
- Can be extended with libraries (CORS, sessions, auth, etc.).

---

## Java and Web

### Jetty

- A **lightweight, embeddable web server and servlet container**.
- Suitable for both development and production use.
- Often used in **embedded Java applications**.
- Supports **servlets**, **WebSockets**, and HTTP/2.

Other Java web servers / containers:
- **Tomcat**
- **GlassFish**
- **WildFly**

---

## Application Server

- provides environment to **run complex, dynamic web applications**.
- Handles:
  - Business logic
  - Session management
  - Resource pooling
  - Database access
  - Security/authentication
- Offers APIs and components to build robust applications.
- Often includes a **web server** or integrates with one.
- Java-based examples:
  - **WildFly (JBoss)**
  - **GlassFish**
  - **WebLogic**
  - **Spring Boot** (self-contained)

**Difference from Web Server:**
- Web Server: Static content and HTTP handling.
- Application Server: Executes application logic (e.g., EJBs, services) and dynamic content.

---