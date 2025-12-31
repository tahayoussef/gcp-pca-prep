# FSI perspective: Reliability

- **High Availability Topology**
    - **Multi-Region**: Deploy across at least **two regions** to withstand regional outages.
    - **Multi-Zone**: Use **three zones** within each region for high availability.
    - **Active-Active**: Use distributed databases like **Spanner** (global consistency) or **Cloud SQL HA** for near-zero RPO.

- **Disaster Recovery (DR)**
    - **Strategy**: Define plans for zonal and regional failures tailored to **RTO/RPO** mandates.
    - **Replication**: Use asynchronous replication for cross-region DR if synchronous is not feasible. Snapshot data to multi-region storage.

- **Operational Resilience**
    - **Regulation**: Meet strict mandates from bodies like the **Federal Reserve** or **EBA**.
    - **Automation**: Automate infrastructure provisioning and recovery to minimize manual errors during failover.
