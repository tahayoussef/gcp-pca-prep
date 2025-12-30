# Case Study: Knight Motives Automotive (v6.1 - IoT & Scale Focus)

## Company Overview
Knight Motives connects millions of vehicles to the cloud. They collect telemetry (speed, engine status, location) to offer "Connected Car" services. 

## Business Requirements
*   **Scale**: Ingest data from millions of vehicles (massive write throughput).
*   **Real-Time**: Insights must be available immediately (e.g., crash detection).
*   **Partner Sharing**: Securely share specific data subsets with Dealerships and Insurers.
*   **Data Residency**: Data must stay in specific regions to comply with local laws.

## Technical Requirements
*   **High Throughput**: "Millions of data points per minute".
*   **Global Layout**: Vehicles are everywhere, but data has locality constraints.
*   **Cost**: Store massive history without breaking the bank.

## Existing Technical Environment
*   **Legacy**: Batch uploads of data to on-prem (Too slow, not real-time).

## Key Services & Architecture Patterns
*   **Ingestion**:
    *   **Cloud Pub/Sub**: The buffer. Decouples the vehicles from the DB. Handles spikes. Global endpoint.
*   **Storage (The Core Question)**:
    *   **Cloud Bigtable**: The ONLY valid answer for "High throughput time-series data at millisecond latency".
        *   *Schema Design*: **Row Key** is critical (e.g., `VehicleID#Timestamp`). Avoid sequential keys to prevent "hotspotting".
    *   **BigQuery**: For analytical queries (Aggregates, trends) on the data exported from Bigtable.
*   **Data Pipeline**:
    *   **Dataflow**: Reads from Pub/Sub -> Writes to Bigtable (Hot path) and BigQuery (Cold/Analytics path).
*   **API to Partners**:
    *   **Apigee**: Create API proxies. Implement **Quotas** (limit partner calls) and **Authentication** (OAuth/API Keys).
*   **Edge**:
    *   **Google Distributed Cloud / Anthos**: If the case study mentions "Processing data inside the car" or "in local dealerships".

## Exam Scenarios & "Gotchas"
*   **Scenario**: "We need to store 5 years of telemetry data for analysis but keep costs low."
    *   **Answer**: Store recent/hot data in **Bigtable**. Use **Dataflow** to downsample/aggregate older data and move it to **BigQuery** (or GCS) for long-term storage.
*   **Scenario**: "Partners need access to data, but we must charge them and limit their usage."
    *   **Answer**: **Apigee** (Monetization + Rate Limiting).
*   **Scenario**: "Ensure European vehicle data never leaves Europe."
    *   **Answer**: Use **Resource Locations** constraints (Org Policy) and ensure Pub/Sub topics and Bigtable instances are Regional (or constrained to EU locations).
*   **Scenario**: "Bigtable performance is slow on writes."
    *   **Answer**: Check for **Row Key Hotspotting** (Sequential IDs). Use **Salting** or **Reverse Domain** keys.
