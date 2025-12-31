# Comparative analysis of Google Cloud deployment archetypes

- **Availability Goals**
    - **Zonal**: 99.9%
    - **Regional**: 99.99%
    - **Multi-regional / Global**: 99.999%

- **Resilience Strategy**
    - **Zonal**: Vulnerable to Zone outage. Needs manual/automated failover to another zone.
    - **Regional**: Resilient to Zone outage. Vulnerable to Region outage.
    - **Multi-regional/Global**: Resilient to Region outage. Lowest RTO (near zero) with synchronous replication.

- **Cost vs Complexity**
    - **Zonal**: Lowest cost, low complexity (but high risk).
    - **Global**: Can be simpler than Multi-regional (fewer objects) but network costs are high.
    - **Hybrid/Multicloud**: Highest complexity and usually highest cost (redundancy, egress, persistent connections).

- **Decision Drivers**
    - **Business Criticality**: High needs -> Multi-regional/Global.
    - **Regulations**: Data Sovereignty -> Regional or Geo-fenced Multi-regional.
    - **Legacy**: On-prem dependencies -> Hybrid.
