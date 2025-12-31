# Oracle PeopleSoft with OCI Exadata

## Overview
Run **Oracle PeopleSoft** applications on **Compute Engine** while using **OCI Exadata** database.

## Architecture
*   **PeopleSoft Application Tier**: Compute Engine VMs (web/app servers).
*   **Database Tier**: Oracle Exadata in OCI.
*   **Connectivity**: Google Cloud Interconnect + OCI FastConnect.

## Use Cases
*   Leverage Exadata's performance for PeopleSoft database.
*   Use Google Cloud for compute, storage, and analytics services.

## Design Considerations
*   **Networking**: Dedicated interconnect; private IP routing.
*   **Latency**: Monitor and optimize for acceptable PeopleSoft performance.
*   **Security**: Secure cross-cloud traffic; IAM on both platforms.
*   **Reliability**: Exadata HA; regional deployment for apps.
*   **Performance**: Connection pooling, caching to minimize cross-cloud calls.

## Best Practices
*   Deploy PeopleSoft app servers close to Exadata (minimize latency).
*   Use Cloud CDN for static content delivery.
