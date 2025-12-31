# Google Cloud zonal deployment archetype

- **Overview**
    - Application runs in a **single zone** within a region.
    - **Availability Target**: 99.9%.

- **Use Cases**
    - Low cost dev/test environments.
    - Applications that can tolerate downtime during zone outages.
    - Batch workloads where data loss is acceptable or checkpoints exist.

- **Design Considerations**
    - **Zone Outages**: Not robust. Application is down if the zone impacts.
    - **Mitigation**: Maintain a passive replica in a **failover zone** (same region) and promote it during outages.
