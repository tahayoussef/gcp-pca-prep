# Networking (Enterprise Foundation Blueprint)

## Overview
The blueprint recommends a secure, private-by-default network architecture using **Shared VPCs** to separate network administration from application deployment. It emphasizes strictly controlled connectivity between environments and on-premises.

## Network Topology Options

### 1. Shared VPC per Environment (Isolated)
*   **Design**: Separate Shared VPCs for Dev, Non-Prod, and Prod.
*   **Traffic**: No direct traffic between environments.
*   **Use Case**: Strict isolation requirements.

### 2. Hub-and-Spoke (Transitive)
*   **Design**: A central **Hub** VPC connects to on-prem and other environment VPCs (Spokes) via Peering or VPN.
*   **Traffic**: Inter-environment traffic flows through the Hub, gated by **Network Virtual Appliances (NVAs)**.
*   **Use Case**: Needs shared services or direct (inspected) paths between environments.

## Connectivity & Security
*   **Hybrid Connectivity**: Use **Dedicated Interconnect** with Global Routing for reliable access to on-premises data centers.
*   **DNS**: Centralized DNS Hub configuration.
    *   **Forwarding Zones**: Cloud resolves on-prem names.
    *   **Inbound Policies**: On-prem resolves Cloud names via the Hub.
*   **Firewalls**:
    *   **Hierarchical Policies**: Enforce organization-wide rules (e.g., block all SSH/RDP from public).
    *   **No Legacy Rules**: Use Network Firewall Policies instead of legacy VPC firewall rules for better management.
*   **Private Connectivity**: No public IPs for workloads. Use **Cloud NAT** for outbound access and **IAP** for administrative access.
