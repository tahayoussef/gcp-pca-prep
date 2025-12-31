# Multi-regional deployment on Compute Engine

- **Architecture**
    - **Multi-Region**: Active-active deployment in **2+ regions** (each region has 3 zones).
    - **Network**: **Global External LB** (Anycast IP) -> Regional MIGs (Web) -> Internal LB -> App.
    - **Database**: Cross-region replication (e.g., PostgreSQL with async replica) or **Multi-region Spanner**.

- **Design Patterns**
    - **Global Routing**: GFE proxies requests to closest region.
    - **DR**: Survival of complete region failure.
    - **Autoscaling**: Regional MIGs autoscale independently based on load.

- **Reliability**
    - **Availability**: 99.999% target.
    - **Latency**: Optimized for end-users via Anycast.
