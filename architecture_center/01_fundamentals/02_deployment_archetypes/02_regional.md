# Google Cloud regional deployment archetype

- **Overview**
    - Application runs across **multiple zones** (typically 3) within a single region.
    - **Availability Target**: 99.99%.
    - **Robustness**: Resilient to zone outages, but not region outages.

- **Use Cases**
    - **Geo-specific**: Users located in a specific country or area.
    - **Latency**: Low latency networking between application components.
    - **Compliance**: Meet **data residency** requirements (e.g., maintain data within Europe).

- **Design Considerations**
    - **Failover**: Use regional load balancing. If a zone fails, traffic routes to other zones.
    - **Region Outage**: Application is down. Requires cross-region DR strategy (passive replica in another region) to recover.
