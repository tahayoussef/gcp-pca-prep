# BigQuery - Comprehensive Guide

## Overview
Serverless, highly scalable, multi-cloud data warehouse.
- **Architecture**: Decoupled **Computer** (Slots) and **Storage** (Colossus). Connected by **Jupiter** network (1 Petabit/sec bisection bandwidth).
- **Format**: Capacitor (Columnar storage format).
- **Access**: SQL (ANSI-2011 compliant).

---

## Optimization: Partitioning vs. Clustering (Exam Critical)

### 1. Partitioning
Divides table into segments.
- **Mechanism**: Physically separates data.
- **Types**:
  - **Ingestion Time**: `_PARTITIONDATE`. Auto-generated based on arrival.
  - **Column-based**: Date or Timestamp column.
  - **Integer Range**: e.g., `Customer_ID` 0-1000, 1001-2000.
- **Benefit**: **Cost Reduction**. Query `WHERE date = '2023-01-01'` only scans that day's partition (Pruning data processed).
- **Limit**: Max 4000 partitions per table.

### 2. Clustering
Sorts data *within* a partition (or table).
- **Mechanism**: Co-locates related data based on sort key (up to 4 columns).
- **Benefit**: **Performance**. Faster filters and aggregations on high-cardinality columns (e.g., `User_ID`, `Email`).
- **Cost**: Also reduces scanning (Block Pruning), but less predictable than partitioning.
- **Use Case**: When you have > 4000 segments needed, or high cardinality filters.

**Rule of Thumb**:
- Filter by Time? -> **Partition**.
- Filter by High Cardinality ID? -> **Cluster**.
- Both? -> **Partition by Time, Cluster by ID**.

---

## Storage & BigLake

### BigQuery Managed Storage
- Standard, internal storage. Optimized for performance.
- **Time Travel**: Access data from past 7 days (`FOR SYSTEM_TIME AS OF ...`).
- **Fail-safe**: 7 days (snapshot).

### BigLake (External Tables)
- Access data residing in **GCS, S3, or Azure Blob Storage**.
- **Key Feature**: Applies BigQuery **Fine-Grained Security** (Row-level, Column-level) to external files.
- **Format**: Parquet, Avro, JSON, CSV.
- **Performance**: Slower than managed storage (no Jupiter optimization), but cheaper storage cost.
- **Metadata Caching**: Can improve listing performance.

---

## Compute (Slots)

### Pricing Models (New "Editions")
- **On-Demand**: Pay per TB scanned. (Default).
- **Editions (Capacity / Slots)**:
  - **Standard**: Basic SQL.
  - **Enterprise**: Advanced security (VPC SC), higher concurrency.
  - **Enterprise Plus**: Highest performance, more features.
  - **Autoscaling**: Slots scale up/down automatically.

---

## Security

1.  **IAM**:
    - `bigquery.dataViewer`: Can read data.
    - `bigquery.jobUser`: Can run queries (consumes slots/cost).
    - **Separation**: Give Analysts `jobUser` (Project A) and `dataViewer` (Dataset B). They run query in A, reading from B. Project A pays.

2.  **Column-Level Security**:
    - Tag columns (Policy Tags).
    - User needs "Data Catalog Fine-Grained Reader" role on the tag to see the column.

3.  **Row-Level Security**:
    - SQL-based filter applied to users.
    - `CREATE ROW ACCESS POLICY ... FILTER USING (region = 'US')`.

---

## Exam Focus Areas

1.  **Cost Optimization**:
    - **Scenario**: "Query costs are too high".
    - Fix: **Partition** the table (reduce bytes scanned).
    - Fix: Use **Materialized Views** (pre-compute aggregations).
    - Fix: `SELECT *` is bad. Select specific columns.

2.  **Performance**:
    - **Scenario**: "Dashboards are slow".
    - Fix: **BI Engine** (In-memory caching layer for BigQuery).

3.  **Real-Time**:
    - **Scenario**: "Need to analyze streaming data immediately".
    - Solution: **Streaming Insert API** (Storage Write API). Data available instantly. (Costly).

4.  **Schema Design**:
    - **Denormalization**: Preferred. Use **Nested and Repeated** fields (Structs/Arrays) instead of many joins. BigQuery loves widetables.
