# Cloud Run - Comprehensive Guide

## Cloud Run - Introduction

### Overview
Cloud Run is a **fully managed serverless platform** for running containerized applications.

**Key Features**:
- **Container to Production**: Takes a container image and runs it as a scalable HTTPS service.
- **Scaling to Zero**: Scales down to 0 replicas when not in use (pay nothing).
- **Concurrency**: Handles **multiple requests per instance** (default 80, configurable up to 1000). This differentiates it from Cloud Functions (1 request per instance).
- **No Ops**: No cluster management, no node management.

---

## Cloud Run - Services vs Jobs

### 1. Cloud Run Services
designed for **long-running services** that respond to HTTP(S) requests.
- **Trigger**: HTTP requests, gRPC, Eventarc (via Pub/Sub, Storage events).
- **Timeout**: Default 5 mins, Max 60 mins.
- **Scaling**: Autoscales based on request concurrency or CPU utilization.
- **Use Case**: REST APIs, Web apps, Microservices.

### 2. Cloud Run Jobs
Designed for **run-to-completion tasks**.
- **Trigger**: Manual, Scheduled (Cloud Scheduler), Workflows.
- **Timeout**: Max 24 hours.
- **Tasks**: Can run array of tasks (e.g., 100 independent tasks) in parallel.
- **Use Case**: Data processing, Database migrations, Batch scripts.

---

## Cloud Run - Concurrency & Scaling

### Concurrency Strategy
**Request-driven Scaling**.
- **Container Instance**: A single VM-like environment running your container.
- **Concurrency Setting**: Max number of requests allowed on one instance at the same time.
- **Scale Out**: When valid requests > (Instances * Concurrency), Cloud Run adds more instances.

**Example**:
- Concurrency = 80 (default).
- Traffic = 100 concurrent requests.
- Cloud Run needs 2 instances (80 on first, 20 on second).

**Optimization**:
- High concurrency (80-200): Better resource utilization, lower cost for I/O bound apps (waiting on DB).
- Low concurrency (1): Strict isolation, high CPU/Memory processing per request.

### Cold Starts & Min Instances
**Cold Start**: Latency when scaling from 0 to 1 instance (loading container).
- **Solution**: Configure **Min Instances = 1** (keeps one instance warm, pay for it).

---

## Cloud Run - CPU Allocation (Billing)

### 1. Request-Based Billing (CPU only during request)
- **Default behavior**.
- **Behavior**: CPU is fully available *only* while processing a request. Outside of requests, CPU is **severely throttled** (approx 5-10%).
- **Pricing**: Pay only when processing requests (rounded up to nearest 100ms).
- **Use Case**: APIs, Websites with sporadic traffic.

### 2. Instance-Based Billing (CPU always allocated)
- **Behavior**: CPU is available 100% of the time, even when idle (background threads run).
- **Pricing**: Pay for the entire lifecycle of the instance (from container start to stop).
- **Use Case**:
  - Background tasks (polling, async processing after response).
  - Steady traffic (often cheaper than request-based if utilization is high).
  - Apps dependent on background agents (e.g., rigid monitoring).

---

## Cloud Run - Networking

### Ingress (Incoming Traffic)
- **All**: Public internet + Internal.
- **Internal**: Only from VPC (Compute Engine, GKE) and Eventarc.
- **Internal and Cloud Load Balancing**: Only from VPC and Cloud Load Balancer (allows WAF/Cloud Armor protection).

### Egress (Outgoing Traffic)
To access resources in a VPC (e.g., Cloud SQL private IP, Memorystore, on-prem via VPN):

**1. Direct VPC Egress** (Recommended):
- Sends traffic directly to VPC.
- **Pros**: Lower latency, higher throughput, lower cost (no connector VMs), simple setup.
- **Cons**: Newer feature, verify region availability.

**2. Serverless VPC Access Connector** (Legacy):
- Provisions dedicated connector instances (hidden VMs) in your VPC.
- **Pros**: Established.
- **Cons**: Cost (pay for connector instances 24/7), potential bottleneck, added latency.

---

## Cloud Run - Revisions and Traffic Splitting

- **Revision**: Immutable snapshot of code + config. Every deployment creates a new Revision.
- **Service URL**: Stable URL points to the service.
- **Traffic Splitting**:
  - Route % of traffic to different revisions.
  - **Canary**: Send 10% to `v2-revision`, 90% to `v1-revision`.
  - **Blue/Green**: instantly switch 100% from `v1` to `v2`.
  - **Rollback**: Instantly switch 100% back to `v1`.

---

## Comparison: Cloud Run vs App Engine vs GKE

| Feature | Cloud Run | App Engine (Standard) | GKE |
| :--- | :--- | :--- | :--- |
| **Workload** | Containerized (Any runtime) | Source Code (Supported runtimes) | Containerized (Complex orchestration) |
| **Ops Model** | Serverless (No nodes) | Serverless (No nodes) | Cluster (Node management in Standard) |
| **Scaling** | 0 to N (Fast) | 0 to N (Fast) | Node pools (Slower) |
| **Timeout** | 60 mins (Service), 24h (Job) | 10 mins (HTTP), 24h (Manual scaling) | Unlimited |
| **VPC Access** | Direct / Connector | Connector | Native |
| **Best For** | Modern Stateless Containers | Legacy Web Apps, rapid dev | Complex Microservices, Stateful app |

---

## Exam Focus Areas

1.  **Serverless Decision**:
    - "Deploy containerized app, no cluster management". -> **Cloud Run**.
    - "Deploy Python code directly, standard web app". -> **App Engine**.
    - "Event-driven function, single purpose". -> **Cloud Functions**.

2.  **VPC Access**:
    - "Cloud Run needs to access Cloud SQL on private IP". -> Configure **Direct VPC Egress** (or Connector).

3.  **Security**:
    - "Only allow internal calls from other GCP services". -> Set Ingress to **Internal**.
    - "Publicly expose but protect with WAF". -> Set Ingress to **Internal and Cloud Load Balancing**, put behind **Global External ALB** with **Cloud Armor**.

4.  **Cost Optimization**:
    - "Sporadic traffic". -> **Request-based billing** (Scale to 0).
    - "Constant high traffic". -> **Instance-based billing** (potentially committed use discounts too).

5.  **Performance**:
    - "Slow startup time (cold start)". -> Set **Min Instances** > 0.
