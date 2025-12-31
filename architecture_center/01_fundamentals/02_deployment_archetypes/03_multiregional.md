# Google Cloud multi-regional deployment archetype

- **Overview**
    - Application runs in **two or more regions**.
    - **Availability Target**: 99.999%.
    - **Robustness**: Resilient to both zone and region outages.

- **Use Cases**
    - **Mission Critical**: Zero downtime requirements (High Availability).
    - **Global/Continental**: Dispersed users needing low latency (closest region).
    - **Compliance**: Can use **geo-fenced routing** to keep traffic within regulatory boundaries (e.g., specific countries in Europe).

- **Design Considerations**
    - **RTO/RPO**: Near-zero RTO if using **synchronous replication** (e.g., Spanner).
    - **Cost/Complexity**: Higher cost for redundant resources and **cross-region data transfer**. Higher operational complexity.
