# Compute Engine - Comprehensive Guide

## Compute Engine - Introduction

### Overview
Compute Engine offers scalable, high-performance **virtual machines (VMs)** running on Google's infrastructure. It provides Infrastructure as a Service (IaaS).

**Key Features**:
- **Custom Machine Types**: Tailor CPU and RAM specific to workload needs
- **Live Migration**: VMs keep running while host maintenance occurs (standard VMs only, not GPUs/Spot)
- **Billing**: Per second (after 1 min minimum)
- **Global**: Deploy in regions/zones worldwide

### Machine Families

**1. General Purpose**:
- **E2**: Cost-optimized, day-to-day computing (web servers, dev/test)
- **N2/N2D**: Balanced performance (databases, caches)
- **C3/C4**: High-performance, new generation

**2. Compute-Optimized (C2, C2D)**:
- High performance per core (gaming, HPC, ad serving)

**3. Memory-Optimized (M1, M2, M3)**:
- Large in-memory databases (SAP HANA), large memory needs

**4. Accelerator-Optimized (A2, A3, G2)**:
- Massively parallel CUDA compute (ML training, inference)

---

## Compute Engine - Lifecycle & Availability

### Instance Lifecycle

**States**:
- **Provisioning**: Allocating resources
- **Staging**: Preparing VM
- **Running**: OS booted
- **Stopping**: Shutdown requested
- **Suspended**: Memory state saved to disk (fast resume)
- **Terminated**: Stopped, no charge for CPU/RAM (storage still billed)

### Availability Policies

**1. Live Migration**:
- Google moves running VM to new host for maintenance without downtime
- **Standard VMs**: Supported
- **GPUs/Spot VMs**: Not supported (Terminate on maintenance)

**2. Automatic Restart**:
- If VM crashes due to hardware failure, restart automatically (default: On)

### Preemptible & Spot VMs

**Spot VMs** (Replacements for Preemptible):
- **Cost**: 60-91% discount
- **Availability**: Spare capacity only; Google can reclaim at any time
- **Grace Period**: **30 seconds** to shut down when reclaimed
- **Duration**: No max duration (Preemptible had 24h max)
- **Use Cases**: Batch jobs, fault-tolerant workloads, stateless apps

**Shutting Down Spot VMs**:
- Use **shutdown scripts** to save state/checkpoint within 30s window
- Detection: Metadata server `maintenance-event` attribute

---

## Compute Engine - Storage Options

### 1. Persistent Disks (Network Block Storage)

**Features**:
- Durable, reliable integration with snapshots
- Network-attached (performance scales with size and machine type)
- **Muti-Writer**: Supported on some SSD types (N2 machines)

**Types**:
- **pd-standard**: HDD (backup, archival)
- **pd-balanced**: SSD (general purpose, best price/performance)
- **pd-ssd**: SSD (high performance databases)
- **pd-extreme**: Provisioned IOPS (highest performance)
- **Hyperdisk**: New generation, decoupled storage/compute optimization

### 2. Local SSD (Ephemeral)

**Features**:
- Physically attached to host server
- **Highest performance** (sub-millisecond latency)
- **Ephemeral**: Data LOST if VM stops/terminates (but survives reboot/live migration)
- **Size**: 375 GB chunks (up to 24 chunks)
- **Use Case**: Scratch disk, cache, NoSQL replication (where durability is software-managed)

### 3. Cloud Storage FUSE

**Features**:
- Mount GCS buckets as file systems on VM
- **High latency** compared to disks
- **Use Case**: Shared repository, large scale unstructured data access (ML training data)

### 4. Filestore (Managed NFS)

**Service Tiers**:
- **Basic (HDD/SSD)**: Single zone, file sharing for general workloads
- **Zonal (High Scale)**: High performance (10-100TiB), genome sequencing
- **Regional (Enterprise)**: High availability (multi-zone), critical apps (SAP)

---

## Compute Engine - Image & Snapshot Management

### Machine Images vs. Snapshots

**Snapshot**:
- Backup of **disk content only**
- Incremental (only stores changes since last snapshot)
- Global availability (stored in Google locations)
- Instant creation (COW - Copy On Write)

**Machine Image**:
- Backup of **entire VM configuration** (Disks + Metadata + Permissions + Settings)
- Used for cloning/replicating VMs exactly

### OS Patch Management (VM Manager)

**VM Manager**: Suite for managing large fleets
- **OS Config Agent**: Must be installed on VM
- **Patch**: Automate OS patching (apt/yum/windows update)
- **Configuration Management**: Enforce state (packages installed, files present)
- **Inventory**: Collect OS details

---

## Compute Engine - Networking

### Network Interface Cards (NICs)

**Default**: Single NIC in `default` VPC (or selected VPC)

**Multi-NIC**:
- **Requirement**: Must be configured **at creation time** (cannot add later)
- **Constraint**: Each NIC must belong to a **different VPC**
- **Use Case**: Appliance separating management/data traffic, or connecting two isolated networks

### Connecting to VMs

**1. Linux (SSH)**:
- **Public IP**: Standard SSH
- **Private IP (IAP)**: Identity-Aware Proxy. **Securest method**. No public IP needed. User explicitly IAM authenticated.

**2. Windows (RDP)**:
- Generate Windows password (stores in metadata)
- Connect via RDP client

**3. Serial Console**:
- Text-based console access for **troubleshooting** (boot issues, network lockouts)
- Requires explicit enable metadata `serial-port-enable=1`

---

## Compute Engine - Managed Instance Groups (MIGs)

### Overview
Group of identical VMs treated as a single entity from an **Instance Template**.

### Types
1. **Stateless MIG**: Auto-scaling web servers (pets vs cattle)
2. **Stateful MIG**: Databases, legacy apps (preserves disk/metadata on instance restart)

### Key Features

**1. Autohealing**:
- Recreates failed instances
- **Health Check**:
  - **Load Balancing HC**: Directs traffic (aggressive)
  - **Autohealing HC**: Recreates VM (conservative). **Exam Tip**: Use separate health checks to avoid restarting VMs just because of a transient latency spike.

**2. Autoscaling**:
- Scale out/in based on:
  - CPU Utilization
  - HTTPS Load Balancing capacity
  - Cloud Monitoring metrics (custom)
  - Pub/Sub queue depth

**3. Regional vs. Zonal**:
- **Zonal**: Single zone (lower cost, lower availability)
- **Regional**: Across 3 zones (higher availability, survives zonal failure)

**4. Updates**:
- **Rolling Update**: Update VMs gradually (e.g., 2 at a time) to minimize downtime
- **Canary Update**: Test new template on % of VMs

---

## Compute Engine - Sole-Tenant Nodes

### Overview
Physical servers dedicated to your project.

### Use Cases
1. **Compliance/Regulatory**: Hardware isolation requirement
2. **Licensing**: Bring Your Own License (BYOL) for per-core licensing (Windows, Oracle)
3. **Performance**: Control over node placement (affinity/anti-affinity)

---

## Compute Engine - Ops Agent

### Overview
Unified agent for **Logging** and **Monitoring**. Replaces legacy Stackdriver Logging/Monitoring agents.

**Capabilities**:
- Collects system metrics (CPU, MEM, Disk) - Basic metrics free, Detailed chargeable
- Collects application logs (syslog, IIS, third-party apps)
- Configured via `config.yaml`
- Powered by **Fluent Bit** (logs) and **OpenTelemetry** (metrics)

---

## Exam Focus Areas

1.  **MIG Autohealing**:
    - Scenario: App freezes but VM is running.
    - Solution: Configure **Application Health Check** (not just port check) in MIG Autohealing policy.

2.  **Private Access**:
    - Scenario: Admin needs to SSH into VM without public IP.
    - Solution: Use **Identity-Aware Proxy (IAP) TCP forwarding**.

3.  **High Availability**:
    - Scenario: Survive zonal failure.
    - Solution: **Regional Managed Instance Group**.

4.  **Storage Choice**:
    - Scenario: High performance scratch data, lost on stop. -> **Local SSD**.
    - Scenario: Shared file system across Linux VMs. -> **Filestore** (or GCS FUSE if read-heavy/archive).
    - Scenario: DB requiring high durability and speed. -> **Hyperdisk** or **Persistent Disk SSD**.

5.  **Cost Optimization**:
    - Scenario: Batch processing job that can be interrupted.
    - Solution: **Spot VMs** (with shutdown script to checkpoint).

6.  **VM Startup/Shutdown**:
    - Metadata `startup-script`: Runs every boot.
    - Metadata `shutdown-script`: Runs on stop/preempt (limited time!).

