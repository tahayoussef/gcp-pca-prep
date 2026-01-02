# Cloud Bigtable - Comprehensive Guide

## Overview
Managed **NoSQL Wide-Column Store**.
- **Use Case**: High throughput, low latency writes/reads (Millions of QPS).
- **Examples**: AdTech (User profiles), IoT (Time-series telemetry), Fintech (Transaction history).
- **Architecture**: Separated Compute (Nodes) and Storage (Colossus).
- **Protocol**: HBase-compatible.

---

## Schema Design (Exam Critical)

### The Row Key
The **ONLY** indexed field. All other lookups are full table scans (slow).
- **Lexicographically Sorted**: Data is stored sorted by Row Key.
- **Goal**: Distribute reads/writes evenly across nodes.

### Hotspotting
When traffic (Reads/Writes) hits a single node (tablet).
- **Anti-Pattern 1**: Starting with **Timestamp** (`2023-01-01_DeviceA`).
  - *Why?* All new data hits the "end" of the table (one node).
- **Anti-Pattern 2**: Starting with **Sequential ID** (`User_1`, `User_2`).
  - *Why?* All new users hit the end.

### Solutions (Key Design Patterns)
1.  **Field Promotion**: Move high-cardinality field to start.
    - Bad: `Timestamp#DeviceID`
    - Good: `DeviceID#Timestamp` (Spreads data by device).
2.  **Reverse Domain Names**:
    - `com.google.maps`, `com.google.search` (Groups related data).
3.  **Salting**:
    - Add random hash/byte to start of key. Guaranteed distribution, but complicates range scans (must scan all salts).

---

## Performance & Scaling

### Storage vs Compute
- **Nodes**: Provide CPU (Query processing).
- **Storage**: Colossus (Disk).
- **Autoscaling**: Can scale based on **CPU Target** (e.g., 70%) or **Storage Target** (2.5TB per SSD node).

### Key Visualizer
- **Diagnostic Tool**: Generates heatmaps of your access patterns.
- **Use Case**: Identify hotspots.
  - *Diagonal Line*: Sequential writes (Timestamp issue).
  - *Horizontal bands*: Specific rows being hammered.

---

## Replication & High Availability
- **Single Cluster**: Zonal availability.
- **Multi-Cluster Routing (App Profile)**:
  - **Type**: "Any Cluster".
  - **SLA**: 99.999% (if buckets are in different zones/regions).
  - **Consistency**: Eventual consistency between clusters.

---

## Exam Focus Areas

1.  **Use Case Selection**:
    - "Time series data, high volume, analytical dashboard" -> **BigQuery** (if analytics dominant) or **Bigtable** (if high throughput writes + point lookups).
    - "Petabyte scale, no relations, sub-10ms latency" -> **Bigtable**.
    - "Transactional, relational" -> **Cloud SQL / Spanner**.

2.  **Correct Row Key**:
    - Question will give 4 options. **Eliminate** any starting with Timestamp. **Select** the one starting with high-cardinality ID (UserID, DeviceID).

3.  **HDD vs SSD**:
    - **SSD**: Default. High performance.
    - **HDD**: "Archive" / "Batch" workloads. rarely used in exam scenarios unless "Cost is #1 factor and latency > 100ms is ok".
