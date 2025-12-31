# Implement zero trust

- **Verify Every Access Attempt Explicitly**
    - Do not trust any user/device inside the perimeter.
    - **Unified Identity**: Use a single IdP (Google Cloud Identity, Active Directory).
    - **Strong Auth**: MFA (Titan Keys) and SSO.
    - **Least Privilege**: Use **Workload Identity Federation** (for GKE/external) and limit Service Account permissions.

- **Secure Your Network**
    - **Access Control**: Use **Identity-Aware Proxy (IAP)** to shift from network perimeter to identity-based access.
    - **Private Connectivity**: Cloud Interconnect, HA VPN, **Private Service Connect**.
    - **Segmentation**: Use **Shared VPC** and **VPC Service Controls** (prevent exfiltration).
    - **Perimeter Defense**: Use **Google Cloud Armor** (DDoS/WAF) and disable default networks.

- **Monitor and Maintain**
    - **Logging**: Centralized logs (Cloud Logging) to detect anomalies.
    - **Network Intelligence Center**: Visualize traffic and performance.
    - **Vulnerability Scanning**: Use **Web Security Scanner** for apps.
    - **Intrusion Detection**: **Cloud IDS** for network threat detection.
