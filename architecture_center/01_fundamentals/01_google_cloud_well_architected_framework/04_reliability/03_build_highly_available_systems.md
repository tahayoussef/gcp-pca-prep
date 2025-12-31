# Build highly available systems through resource redundancy

- **Principle Overview**
    - **Redundancy**: Replicate critical components to avoid single points of failure (SPOF).
    - **Scope**: Redundancy must exist across Machines, Zones, and Regions.

- **Identify Failure Domains and Replicate**
    - **Failure Domains**: diverse scopes where failure can occur (e.g., a single VM, a Zone, a Region).
    - **Strategy**: Map domains and replicate services across them (e.g., Multi-Zonal or Multi-Regional deployments).
    - **Automation**: Use **Managed Instance Groups (MIGs)** and Load Balancers for automatic failover.

- **Detect and Address Issues**
    - **Monitoring**: Continuous tracking using **Google Cloud Service Health**.
    - **Health Checks**: Configure Load Balancers to detect unhealthy backends and route traffic elsewhere.
