# Google Cloud global deployment archetype

- **Overview**
    - Application serves users globally using **global resources** (e.g., Global Load Balancer, Cloud Spanner).
    - **Availability Target**: 99.999%.

- **Use Cases**
    - **Global Audience**: Applications serving users worldwide with high availability.
    - **Simplified Ops**: Manage fewer global resources instead of many regional shards.

- **Design Considerations**
    - **Cost**: Can be cheaper than multi-regional due to simplified management, but **Global Load Balancer** requires Premium Tier network pricing.
    - **Networking**: High volume of cross-location traffic leads to higher networking costs.
    - **SPOF**: Must careful manage changes to global configurations to avoid global outages.
