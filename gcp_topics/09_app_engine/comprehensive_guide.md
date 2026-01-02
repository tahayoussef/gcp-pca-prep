# App Engine - Comprehensive Guide

## App Engine - Introduction

### Overview
Fully managed, serverless platform for building and hosting web applications.

**Key constraints (Exam Focus)**:
- **One App Engine Application per Project**.
- **Region is Permanent**: You select the region when you create the app; it **cannot be changed**.
- **Hierarchy**: Application -> Services -> Versions -> Instances.

---

## App Engine Environments: Standard vs. Flexible

### 1. Standard Environment
Optimized for **quick scaling** and **low cost**.
- **Architecture**: Runs in a **sandbox**.
- **Languages**: Specific supported versions (Python, Java, Node.js, Go, PHP, Ruby).
- **Startup**: **Milliseconds**.
- **Scaling**: Scales to **Zero** (free).
- **Network**: Cannot access Compute Engine/VPC resources (requires Serverless VPC Connector).
- **Use Case**: Web apps with spiky traffic, APIs, rapid scaling needs.

### 2. Flexible Environment
Optimized for **flexibility** and **custom runtimes**.
- **Architecture**: Runs **Docker containers** on Compute Engine VMs (health checked/managed by App Engine).
- **Languages**: Any (via Dockerfile).
- **Startup**: **Minutes** (VM boot time).
- **Scaling**: **Minimum 1 instance** (Costs even if idle).
- **Network**: Runs *inside* your VPC (native access to Compute Engine resources).
- **Use Case**: Custom libraries (C++ binaries), background threads, consistent traffic.

---

## App Engine scaling

### 1. Automatic Scaling
**Default**.
- **Triggers**: Request latency, CPU, Throughput.
- **Behavior**: Creates instances as needed, shuts them down after idle (approx 15 mins).
- **Min/Max**: Can configure `min_instances` (to avoid cold start) and `max_instances` (cost control).

### 2. Basic Scaling
- **Behavior**: Creates instances when requests arrive. Shuts down when idle.
- **Limit**: Max instances limit is enforced.
- **Use Case**: Simple apps, irregular traffic, development.

### 3. Manual Scaling
- **Behavior**: Run a specific number of instances continuously.
- **Lifecycle**: Instances run indefinitely (even without traffic).
- **Use Case**: Workers processing tasks, complex initialization apps.

---

## Traffic Splitting (Canary Deployments)

**Feature**: Shift traffic between different **Versions** of a **Service**.

**Methods**:
1.  **IP Address (Default)**: Hashes client IP. Sticky user experience.
2.  **Cookie**: Sets a specific cookie. More precise control.

**Workflow**:
1.  Deploy new code as a new Version (v2).
2.  Split traffic: 90% to v1, 10% to v2.
    ```bash
    gcloud app services set-traffic my-service \
      --splits v1=.9,v2=.1
    ```
3.  Monitor error rates.
4.  Migrate 100% to v2.

---

## Configuration (`app.yaml`)

**Core File**: Defines runtime, scaling, handlers (URL routing).

```yaml
runtime: python39
service: default

# Handlers: URL routing
handlers:
- url: /static
  static_dir: static
- url: /.*
  script: auto

# Scaling (Optional - generally stick to automatic default)
automatic_scaling:
  target_cpu_utilization: 0.65
  min_instances: 1
```

---

## Exam Focus Areas

1.  **Standard vs Flexible**:
    - **Scenario**: "Scale to zero, minimize cost". -> **Standard**.
    - **Scenario**: "Needs custom C++ library" or "Needs to modify kernel parameters" or "Long running background process". -> **Flexible**.
    - **Note**: If "Cloud Run" is an option for custom containers, it is often preferred over Flex today.

2.  **Traffic Splitting**:
    - **Scenario**: "Test new version on small % of users". -> **Traffic Splitting (Canary)**.
    - **Mechanism**: **IP Address** splitting is simplest, **Cookie** splitting is more robust for mobile/NAT users.

3.  **One per Project**:
    - **Scenario**: "Deploy App Engine in US and EU". -> **Impossible** in one project. Create **Two Projects**.

4.  **VPC Access**:
    - **Standard**: Needs **Serverless VPC Access Connector** to reach Cloud SQL private IP.
    - **Flexible**: Native access (runs in VPC).
