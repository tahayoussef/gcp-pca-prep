# Google Kubernetes Engine (GKE) - Comprehensive Guide

## GKE - Overview & Architecture

### What is GKE?
Managed Kubernetes service for deploying, managing, and scaling containerized applications.

### Cluster Architecture

**1. Control Plane (Master)**:
- Managed by Google (hidden/abstracted)
- Runs API Server, Scheduler, Controller Manager, etcd
- Endpoint: Public Endpoint (default) or Private Endpoint (private cluster)

**2. Worker Nodes**:
- Compute Engine VMs that run your workloads (Pods)
- Managed by GKE (upgrades, repairs) but visible in Compute Engine (for Standard)

### Admin Management Models

**1. GKE Standard** (Classic):
- **You manage**: Nodes (machine types, upgrades/maintenance windows)
- **Billing**: Pay for underlying Nodes (VMs) even if empty
- **Flexibility**: Maximum configurability (custom machine types, specific system configurations)

**2. GKE Autopilot** (Recommended/Default):
- **Google manages**: Entire infrastructure (nodes, scaling, security)
- **Billing**: Pay for **Pods** (vCPU/Memory requested) only
- **Best Practices**: Security hardened by default, eliminates node management
- **Production Ready**: Optimized for production out of the box

---

## GKE - Cluster Networking

### 1. VPC-Native Clusters (Alias IPs)
**Default & Recommended Mode**.

**How it works**:
- Pods get IP addresses from a **secondary range** of the VPC subnet.
- **Benefits**:
  - **Native Routing**: Pod IPs are routable inside VPC and over VPN/Interconnect (access on-prem).
  - **No Route Quotas**: Doesn't use legacy static routes (avoid quota limits).
  - **Performance**: High throughput, supports Container-Native Load Balancing (NEGs).

### 2. Routes-Based Clusters (Legacy)
- Uses static routes table. **Avoid**. Limited scale.

### 3. Private Clusters
**Security Best Practice**.

**Architecture**:
- **Nodes**: Have **only private IP addresses** (no public Internet access). require Cloud NAT for outbound access.
- **Control Plane**:
  - **Private Endpoint**: Accessible only from VPC/Authorized Networks.
  - **Public Endpoint**: Optional (can disable), or restricted via authorized networks.

---

## GKE - Scaling Mechanisms

### 1. Workload Scaling (Pod Level)

**Horizontal Pod Autoscaler (HPA)**:
- **Scale Out**: Adds more **Pods** replicas.
- **Triggers**: CPU, Memory, Custom Metrics (Cloud Monitoring).

**Vertical Pod Autoscaler (VPA)**:
- **Scale Up**: Increases **CPU/Memory requests** for existing pods.
- **Mode**: "Off" (recommend only), "Initial", "Auto" (terminates and recreates pod with new size).
- **Conflict**: Generally don't use with HPA on same metric (CPU/Mem).

### 2. Infrastructure Scaling (Node Level)

**Cluster Autoscaler (CA)**:
- **Scale Node Pools**: Adds/removes **Nodes** in a node pool.
- **Trigger**: **Pending Pods** (pods that cannot be scheduled due to lack of resources).
- **Downscale**: Removes nodes if underutilized and pods can move elsewhere.

**Node Auto Provisioning (NAP)**:
- **Create Node Pools**: Automatically creates **new node pools** with efficient machine types.
- **Example**: If a pending pod needs 64GB RAM and no existing pool fits efficiently, NAP creates a High-Mem node pool.
- **Boundary**: Respects cluster-level resource limits (e.g., max 1000 CPUs).

---

## GKE - Security

### 1. Workload Identity
**Mechanism**: Maps Google Service Account (GSA) to Kubernetes Service Account (KSA).

**Workflow**:
1. Create GSA with IAM roles (e.g., Storage Object Viewer).
2. Create KSA.
3. Bind GSA to KSA via IAM policy binding (`roles/iam.workloadIdentityUser`).
4. Annotate KSA with GSA email.
5. Pod uses KSA → Authenticates as GSA → Accesses GCP APIs.

**Benefit**: No secrets/keys needed inside Pods. Granular permissions.

### 2. Binary Authorization
**Supply Chain Security**.
- Ensures only **trusted images** are deployed.
- **Attestations**: verifies images were built by trusted CI/CD, scanned for vulnerabilities, and approved.
- **Policy**: "Allow all", "Disallow all", "Require Attestations".

### 3. Network Policy
**Firewall for Pods**.
- Controls traffic flow **between Pods**.
- Default: All pods can talk to all pods.
- Policy: Restrict traffic (e.g., Frontend can call Backend, but not Database directly).

---

## GKE - Storage (CSI)

### Container Storage Interface (CSI)
Standard interface for storage. GKE supports:
- **Compute Engine PD CSI**: ReadWriteOnce (RWO) - Block storage.
- **Filestore CSI**: ReadWriteMany (RWX) - NFS shared storage.
- **Cloud Storage FUSE CSI**: ReadWriteMany/ReadOnlyMany - Object storage as file system.

### StatefulSets
- Workload API for stateful apps (databases).
- Guarantees: Stable network ID (`web-0`, `web-1`), stable persistent storage.

---

## GKE - Ingress & Load Balancing

### Ingress
- Exposes HTTP(S) services to Internet.
- **GKE Ingress Controller**: Automatically creates **Google Cloud Application Load Balancer** (Global External ALB).
- Supports: SSL termination, path-based routing, multi-cluster ingress (MCI).

### Service Types
- **ClusterIP**: Internal only (default).
- **NodePort**: Exposes on static port on each Node IP.
- **LoadBalancer**: Creates classic Network Load Balancer (avoid for HTTP) or Proxy LB.

### Container-Native Load Balancing (NEG)
- Traffic goes **Load Balancer → Pod** directly (skips Node proxying).
- Requires VPC-native cluster.
- **Benefits**: Lower latency, better visibility, pod-level health checks.

---

## Exam Focus Areas

1.  **Autopilot vs Standard**:
    - **Scenario**: "Minimize operational overhead", "Security best practices by default". -> **Autopilot**.
    - **Scenario**: "Need custom kernel modules", "Need to manage node OS upgrades". -> **Standard**.

2.  **Private Clusters**:
    - **Scenario**: "Strict security requirements", "No public IPs on nodes". -> **Private Cluster** + **Cloud NAT** (for outbound access).

3.  **Scaling**:
    - **Scenario**: "Pods are crashing due to OOM (Out of Memory)". -> **VPA** (to resize requests).
    - **Scenario**: "Sudden traffic spikes need more capacity". -> **HPA** (pods) + **Cluster Autoscaler** (nodes).
    - **Scenario**: "Different workloads need different machine types automatically". -> **Node Auto Provisioning**.

4.  **Workload Identity**:
    - **Scenario**: "Pod needs to access BigQuery". -> **Workload Identity** (bind KSA to GSA). **NEVER** use service account keys in container.

5.  **Multi-Cluster**:
    - **Scenario**: "Unified ingress for clusters in US, EU, Asia". -> **Multi-Cluster Ingress (MCI)**.

6.  **VPC-Native**:
    - **Scenario**: "Need to access Pod IPs from on-premise VPN". -> **VPC-Native** (Alias IPs).

7.  **Binary Authorization**:
    - **Scenario**: "Ensure only scanned images are deployed". -> **Binary Authorization**.
