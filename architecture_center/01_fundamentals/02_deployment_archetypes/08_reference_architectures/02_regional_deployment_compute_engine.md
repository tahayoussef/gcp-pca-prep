# Regional deployment on Compute Engine

- **Architecture**
    - **Active-Active**: Stack deployed across **3 zones** within a region.
    - **Network**: Regional External LB -> Regional MIG (Web) -> Regional Internal LB -> Regional MIG (App).
    - **Storage**: **Regional Persistent Disks** (Sync replication across 2 zones).
    - **Database**: HA Database (Primary + Standby in different zones) or Cloud SQL HA.

- **Design Patterns**
    - **Zonal Resilience**: If one zone fails, LB routes to other zones.
    - **Data Protection**: Sync replication ensures near-zero RPO for zone failure.

- **Reliability**
    - **Availability**: 99.99% target.
    - **Region Outage**: Application is down if the whole region fails. Requires multi-region strategy for higher availability.
