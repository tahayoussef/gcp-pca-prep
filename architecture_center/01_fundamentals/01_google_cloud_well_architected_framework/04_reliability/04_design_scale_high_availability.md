# Build highly available systems through resource redundancy

- **Principle Overview**
    - Avoid single points of failure.
    - Replicate critical components across multiple machines, zones, and regions.
    - Ensure global availability by not relying on a single zone/region.

- **Identify Failure Domains and Replicate**
    - Map specific **failure domains** (VM, Zone, Region).
    - Design redundancy across these domains.
    - Configure **automatic failover** for apps and services.

- **Detect and Address Issues**
    - Monitor status using **Google Cloud Service Health** and **Personalized Service Health**.
    - Use **Load Balancers** with health checks to route traffic away from unhealthy backends.

- **Test Failover Scenarios**
    - Regularly simulate failures ("fire drills") to validate recovery.
    - Simulate zonal outages for **MIGs** and **GKE** clusters.
