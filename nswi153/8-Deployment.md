# Deployment

Deployment is the process of **delivering software to a runtime environment** — such as staging, production, or test servers.

---

## Manual copying

Simple but primitive method of deployment.

- Tools: `WinSCP`, `SCP`, `rsync`, `FTP`, or manual `SSH`.
- **Pros**:
  - Very simple to understand.
  - No setup required beyond access to the server.
- **Cons**:
  - Manual and error-prone.
  - Not scalable.
  - Only suitable for **single environments** or small apps.

---

## Deployment script
A custom script that automates steps like copying files, restarting services, building the app, etc.

- **Pros**:
  - Repeatable and shareable with teammates.
  - Can be committed to version control.
- **Cons**:
  - Still relatively basic.
  - May need extra tools for error handling or logging.

---

## Ansible
An **IT automation tool** that simplifies deployment, configuration, and orchestration.

- Uses **YAML playbooks** to define repeatable steps (e.g., install packages, configure files, restart services).
- Agentless: Only requires SSH and Python on the remote server.

- **Pros**:
  - Fully automated and idempotent (safe to run multiple times).
  - Scales well across many servers/environments.
- **Cons**:
  - Learning curve.
  - Might be overkill for very small projects.

---

## Webhook

A **webhook** triggers a deployment when a certain event happens, like a `git push`.

- Often configured to send a `POST` or `GET` request to a deployment script or server endpoint.
- Can integrate with GitHub, GitLab, Bitbucket, etc.

-  **Pros**:
  - Automated and event-driven.
  - Easy setup for small teams or projects.
- harder to test it locally

---

## Deploying New Versions

### Blue-Green Deployment

- Maintain two environments: **blue** (current) and **green** (new).
- Deploy to green, test it, then switch traffic from blue to green.
- Zero downtime, easy rollback.

### Canary Deployment

- Gradually roll out the new version to a **subset of users**.
- Monitor for errors or issues before full release.
- Safer for large user bases.
- More complex to manage (requires traffic routing or feature flagging).

--- 

## DevOps
- A cultural and technical movement that combines **development (Dev)** and **operations (Ops)**.
- Focuses on:
  - **Collaboration** between teams.
  - **Automation** of build, test, and deployment processes.
  - **Continuous Integration / Continuous Deployment (CI/CD)**.
- Goal: Deliver software **faster**, **more reliably**, and **more frequently**.

---

## Virtual Machine
- Software emulation of a **physical computer**.
- Runs a full operating system in an isolated environment.
- Heavier than containers (includes its own OS kernel).
- Tools: VirtualBox, VMware, Hyper-V.

---

## Docker

A platform for creating, deploying, and managing **containers**.

- Uses **Linux namespaces** and **cgroups** for isolation.
- Provides **lighter-weight** virtualization than VMs.
- Docker on Windows uses **WSL (Windows Subsystem for Linux)** under the hood.
- **Image**: A snapshot of a container (code, dependencies, metadata).
- **Container**: A running instance of an image.

### Key Points:
- Faster startup than VMs.
- Better resource utilization.
- Cross-platform (Linux-first).

### Alternatives:
- **Podman** – rootless container engine, compatible with Docker CLI.

---

## Multi-state build

- Defined using multiple `FROM` instructions in a `Dockerfile`.
- Each `FROM` starts a **new stage**.
- Allows you to:
  - Build dependencies/tools in one stage.
  - Copy only the final output to the next stage.
- Final image is **smaller** and **more secure**.

---

## Docker Compose
- Tool to define and run **multi-container Docker applications**.
- Uses a `docker-compose.yml` file to:
  - Define services, networks, and volumes.
  - Bring up complex stacks with a single command.

---

## Docker swarm
- Native Docker **orchestration tool** for running containers across multiple machines.
- Supports load balancing, service scaling, and failover.
- Simpler than Kubernetes, but less feature-rich.

---

## Kubernetes

- Open-source container **orchestration platform**.
- Manages **deployment**, **scaling**, and **networking** of containerized applications.
- Uses a YAML-based configuration (like Docker Compose, but more powerful).
- Supports:
  - Rolling updates
  - Auto-healing
  - Horizontal scaling
  - Multi-node clusters
- Industry standard for **large-scale container orchestration**.

---

## Nomad
- A **lightweight, flexible orchestrator** developed by HashiCorp.
- Supports **Docker**, **VMs**, and **raw binaries**.
- Simpler and faster to set up than Kubernetes.
- Good for **heterogeneous workloads**.

---

## GitHub Actions

- A **CI/CD tool** integrated into GitHub.
- Allows automation of workflows (build, test, deploy) on **git push**, **PRs**, etc.
- Defined in `.github/workflows/*.yml`.

# Some terminology

## On-premise 
- Software or infrastructure that runs on **your own servers or local machines**.
- You manage everything: hardware, networking, updates, security.


## Infrastructure as a service (IaaS)
- Provides **virtualized computing resources** over the internet.
- You manage:
  - Operating system
  - Applications
  - Middleware
- Provider manages:
  - Servers
  - Storage
  - Networking
### Examples:
- AWS EC2
- Microsoft Azure Virtual Machines
- Google Compute Engine


## Platform as a Service (PaaS)

- Higher-level abstraction than IaaS.
- You focus on **your code**, the platform handles:
  - OS
  - Middleware
  - Runtime
  - Infrastructure

### Examples:
- Heroku
- Google App Engine
- Azure App Service


## Software as a Service (SaaS)

- Software is hosted and maintained by a provider, accessible over the internet.
- You just use the application — **no infrastructure management**.

### Examples:
- Gmail
- Dropbox
- Salesforce
- Google Docs


## Function as a Service (FaaS) / Serverless

- A form of cloud computing where you write **individual functions**, and the provider runs them **on-demand**.
- You are charged **only when the function executes**.
- Great for **event-driven** systems and minimizing cost.

### Examples:
- AWS Lambda
- Azure Functions
- Google Cloud Functions