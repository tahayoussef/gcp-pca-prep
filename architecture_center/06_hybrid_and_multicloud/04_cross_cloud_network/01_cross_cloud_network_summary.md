# Cross-Cloud Network for Distributed Applications

## Connectivity Options
*   **Network Connectivity Center (NCC)**: Hub for centralized network management across Google Cloud, on-prem, and other clouds.
*   **Cloud VPN**: IPsec VPN tunnels for encrypted connections.
*   **Router Appliances**: Third-party NVAs (network virtual appliances) for advanced routing/security.

## Service Networking
Expose services across environments using:
*   **Private Service Connect**: Private access to Google Cloud services from on-prem/other clouds.
*   **Service Mesh** (Anthos Service Mesh): Consistent service-to-service communication across environments.

## Security
*   **Encryption**: All cross-cloud traffic encrypted.
*   **Firewall Rules**: Control traffic between environments.
*   **IAM**: Centralized identity management

.

## Reference Architectures
*   **NCC + VPN**: Google Cloud ↔ on-prem/other clouds via VPN.
*   **NCC + Router Appliance**: Advanced routing (BGP) with third-party NVAs.
*   **VPN Only**: Simpler setup for basic hybrid connectivity.
