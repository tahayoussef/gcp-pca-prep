# Continuous Data Replication to BigQuery using Striim

## Overview
Use **Striim** (third-party streaming ETL platform) for **Change Data Capture (CDC)** and continuous replication from operational databases to **BigQuery**.

## Architecture
*   **Source Database**: MySQL, PostgreSQL, Oracle, SQL Server (on-prem or cloud).
*   **Striim**: Captures database changes via transaction logs (CDC).
*   **BigQuery**: Target data warehouse.

## How It Works
1.  **Initial Load**: Striim performs full table copy from source to BigQuery.
2.  **CDC Stream**: Striim monitors database transaction log for changes (INSERTs, UPDATEs, DELETEs).
3.  **Real-Time Replication**: Changes streamed to BigQuery in near real-time.
4.  **Transformation**: Optional in-flight transformations (filtering, enrichment).

## Use Cases
*   **Operational Analytics**: Real-time analytics on operational data.
*   **Database Migration**: Migrate to BigQuery with minimal downtime.
*   **Data Integration**: Integrate multiple heterogeneous databases.

## Benefits
*   **Low Latency**: Near real-time data availability.
*   **Minimal Impact**: CDC reads from transaction logs, not production tables.
*   **Schema Evolution**: Handles schema changes automatically.

## Setup
1.  Deploy Striim on Compute Engine or GKE.
2.  Configure source database connection (enable binary logging/transaction logs).
3.  Create Striim CDC pipeline.
4.  Configure BigQuery target.
5.  Monitor pipeline in Striim UI.
