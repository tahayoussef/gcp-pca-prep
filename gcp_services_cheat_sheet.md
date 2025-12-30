# GCP PCA Services Cheat Sheet: Deep Dive Edition

A comprehensive guide focusing on exam-critical details, differentiators, and decision points.

## 1. Compute
### Compute Engine (GCE)
*   **Machine Types**:
    *   *E2/N2/N2D*: General purpose.
    *   *C2*: Compute-optimized (High performance computing, gaming).
    *   *M1/M2*: Memory-optimized (SAP HANA, large in-memory DBs).
    *   *A2*: Accelerator-optimized (ML/GPU).
*   **Live Migration**: Google moves your VM to a new host during maintenance *without downtime*. **Exam Tip**: Only GCE supports this; AWS/Azure reboot.
*   **Preemptible vs Spot**:
    *   *Preemptible*: Max 24h run time. 30-sec termination notice. Fixed price discount.
    *   *Spot*: No max run time. Dynamic pricing. 30-sec termination notice.
    *   *Use Case*: Batch jobs, fault-tolerant workloads, GKE node pools.
*   **Sole Tenant Nodes**: Physical server dedicated to you. Use for **BYOL** (Bring Your Own License) or strict **Compliance** (no noisy neighbors).
*   **Shielded VMs**: Verifies boot integrity (vTPM) + integrity monitoring.

### Google Kubernetes Engine (GKE)
*   **Modes**:
    *   *Standard*: You manage nodes. Best for custom machine types, GPUs, transparency.
    *   *Autopilot*: Google manages nodes (hidden). Best for ops-minimized production, security best practices by default.
*   **Network**: By default, uses VPC-native (Alias IPs). Pods get IPs from a secondary subnet range.
*   **Multi-Cluster**: use **Anthos (GKE Enterprise)** for multi-cloud or hybrid. **Multi-Cluster Ingress (MCI)** for global load balancing across clusters.
*   **Binary Authorization**: Ensure only trusted/signed images are deployed.

### App Engine (GAE)
*   *Standard*: Language sandboxes (Python, Java, Go, etc.). **Scales to zero**. Seconds to start. cannot write to local disk (use /tmp but it's RAM).
*   *Flexible*: Docker containers. Minutes to start. Can access local disk. Can run background threads longer. **Minimum 1 instance**.

### Cloud Run
*   **Concurrency**: One container instance can handle *multiple* requests (unlike AWS Lambda default).
*   **Direct VPC Egress**: Access VPC resources (Cloud SQL, Memorystore) without a connector (new feature, but connector usually tested).
*   **Trigger**: HTTPS or Eventarc (Pub/Sub, Audit Logs).

### Cloud Functions
*   **Gen 1 vs Gen 2**: Gen 2 is built on Cloud Run (longer timeouts, larger instances, traffic splitting).
*   **Use Case**: "Glue code", light ETL, answering webhooks.

---

## 2. Storage
### Cloud Storage (GCS)
*   **Consistency**: Strong global consistency for *all* operations (read-after-write, overwrite, delete).
*   **Classes & Minimums**:
    *   *Standard*: No min duration.
    *   *Nearline*: 30 days min storage duration. Data retrieval fee.
    *   *Coldline*: 90 days. Higher retrieval fee.
    *   *Archive*: 365 days. Highest retrieval fee.
*   **Lifecycle Policies**: Automate transition (Standard -> Nearline -> Archive -> Delete) based on Age, CreatedBefore, etc.
*   **Versioning**: Protects against accidental overwrite/delete.
*   **Retention Policy**: "Bucket Lock". WORM (Write Once Read Many). Compliance requirement for preventing deletion.

### Persistent Disk (PD)
*   **Regional PD**: Replicated across 2 zones. If one zone fails, you force-attach to a VM in the other zone. **Exam Tip**: Key for HA database architectures on GCE.
*   **Local SSD**: Ephemeral, physically attached. Extreme performance / IOPS. Data *lost* on stop/terminate (but survives reboot/live migration).
*   **Snapshots**: Incremental, global (or regional).

### Filestore
*   *Tiers*:
    *   *Basic*: Standard/HDD or Premium/SSD. NFSv3.
    *   *High Scale / Enterprise*: High performance, critical apps.
*   *Use Case*: Legacy apps needing `open()`, `read()`, `write()` posix semantics.

---

## 3. Databases (The "Pick the Right DB" Question)
*   **Cloud SQL**
    *   *Engine*: MySQL, PostgreSQL, SQL Server.
    *   *Capacity*: Up to ~64TB. Vertical scale (resize VM).
    *   *HA*: Regional (Primary + Standby in different zone). Synchronous replication.
    *   *Read Replicas*: For scaling *reads* only. Asynchronous.
    *   *Exam Tip*: "Lift and shift existing SQL DB" -> Cloud SQL.
*   **Cloud Spanner**
    *   *Keywords*: Global, Horizontal Scale, Strong Consistency, Financial data, 99.999% SLA.
    *   *Wait*: It's SQL (ANSI 2011), but creating it is expensive ($$$).
    *   *Exam Tip*: "Outgrown Cloud SQL" or "Global Consistency" -> Spanner.
*   **BigQuery**
    *   *Keywords*: Data Warehouse, Analytics, SQL, Petabytes, Serverless.
    *   *Storage*: Columnar (Capacitor). Compute/Storage separated.
    *   *Partitioning*: By time or integer. Improves performance/cost by scanning less data.
    *   *Clustering*: Sorts data within partitions.
*   **Cloud Bigtable**
    *   *Keywords*: IoT, Time-series, Ad-Tech, High Write Throughput (ms latency), HBase API.
    *   *Anti-pattern*: SQL queries, complex joins, multi-row transactions (only supports single-row tx).
    *   *Key Design*: Avoid "Hotspotting" (sequential keys). Use Hashed keys or Reverse/Salted keys.
*   **Firestore**
    *   *Keywords*: Mobile apps, real-time sync, offline documents, hierarchal data.
    *   *Datastore Mode*: Backward compatible with Datastore. Good for server backend hierarchical data.
*   **Memorystore**
    *   *Redis/Memcached*. In-memory cache. Reduces database load.

---

## 4. Networking
### VPC
*   **Global**: VPCs span the globe. Subnets are Regional.
*   **Shared VPC**:
    *   *Host Project*: One network admin team manages the network.
    *   *Service Project*: Developers use subnets but can't change FW rules.
    *   *Separation of Duties*: Security manages network; Devs manage instances.
*   **VPC Peering**: Decentralized. Connect two independent VPCs. *Non-transitive* (A peers B, B peers C -> A cannot reach C).
*   **Private Google Access**: Allow VMs with *internal IP only* to reach Google APIs (GCS, BigQuery) without a NAT gateway.

### Load Balancing
*   **Global External HTTP(S) LB**: Anycast IP. Terminates SSL at the edge.
*   **Cloud Armor**: Attach to HTTP(S) LB for DDoS, SQLi, XSS protection.
*   **Internal HTTP(S) LB**: Layer 7 balancing for internal microservices.

### Hybrid Connectivity
*   **Cloud VPN**: 3 Gbps limit per tunnel. ECMP for higher throughput.
*   **Dedicated Interconnect**: 10 Gbps or 100 Gbps physical link. SLA. Low latency.
*   **Partner Interconnect**: You connect to a partner (ISP), they connect to Google. Good if you don't need full 10Gbps or aren't at a peering location.
*   **Direct Peering**: NOT for GCP resources (Compute/Storage). It's for G-Suite/YouTube.

---

## 5. IAM & Security
*   **Identity**: `Google Cloud Directory Sync (GCDS)` syncs AD users/groups to Cloud Identity.
*   **Service Accounts**:
    *   *Best Practice*: Don't download keys (`.json`) unless absolutely necessary (e.g., on-prem app). On GCP, use attached Service Accounts.
    *   *Scopes vs IAM*: Scopes are legacy. Use "Allow Full Access" scope and restrict via IAM Roles.
*   **Workload Identity**: Map K8s Service Account (KSA) -> Google Service Account (GSA). Removes need for Kubernetes Secrets for keys.
*   **IAP (Identity-Aware Proxy)**:
    *   *TCP Forwarding*: SSH/RDP to private VMs without Bastion Host/VPN.
    *   *Web App*: AuthN/AuthZ layer before your web app.
*   **Organization Policies**: Constraints on resources. (e.g., "Restrict VM external IP", "Restrict allowed regions"). **Exam Tip**: Use this for compliance guardrails.

---

## 6. Operations (SRE)
*   **Cloud Monitoring**: "White box" monitoring (CPU, RAM, App metrics).
    *   *Uptime Checks*: "Black box" monitoring (Ping from outside).
    *   *Group*: Treat a MIG as a single entity.
*   **Cloud Logging**: Structured logging (JSON).
    *   *Sinks*: Operations (30 days) -> GCS (Archive), BigQuery (Analytics), Pub/Sub (Splunk/3rd party).
*   **Cloud Trace**: Find latency bottlenecks in microservices.
*   **Cloud Profiler**: Find CPU/Memory hotspots in code.

---

## 7. Data & ML Pipeline Patterns
*   **Ingest**: Pub/Sub (Streaming) or Transfer Appliance (Massive batch > 20TB).
*   **Process**: Dataflow (Transform/Enrich).
*   **Store**: BigQuery (Analytics) or Bigtable (High speed).
*   **ML**: Vertex AI.
    *   *AutoML*: Low code, standard tasks (Classify images, sentiment analysis).
    *   *Custom Training*: You write TensorFlow/PyTorch code.
