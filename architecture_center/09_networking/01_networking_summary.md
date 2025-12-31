# Networking

## Best Practices for VPC Design
*   **IP Planning**: Use RFC 1918 private IPs; plan for growth; avoid overlaps with on-prem.
*   **Subnets**: One subnet per region; use secondary ranges for GKE pods/services.
*   **Firewall Rules**: Least-privilege; use tags/service accounts for targeting.
*   **Shared VPC**: Centralized network management; host project provides networking for service projects.
*   **VPC Peering**: Connect VPCs within Google Cloud (transitive peering not supported).

## Connect

### Hub-and-Spoke VPC Topology
*   **Hub**: Central VPC for shared services (DNS, NVAs, egress).
*   **Spokes**: VPCs for individual applications/teams.
*   **Connectivity**: VPC Peering or VPN between hub and spokes.
*   **Benefits**: Centralized control, simplified routing, cost savings (shared NAT/egress).

### Connecting Other CSPs
*   **VPN**: Encrypted tunnels between Google Cloud and AWS/Azure.
*   **Dedicated Interconnect**: Physical connection via colocation.
*   **Partner Interconnect**: Via connectivity partners (Equinix, Megaport, etc.).

## Secure

### FortiGate Architecture
*   **FortiGate NGFW**: Third-party firewall/IDS/IPS on Compute Engine.
*   **Deployment**: Active-passive HA; routes traffic through FortiGate for inspection.

### Palo Alto Networks NGFW
*   **VM-Series**: Palo Alto firewall on Compute Engine.
*   **Use**: Advanced threat protection, URL filtering, application control.

### GCVE Advanced Network Security
*   **Google Cloud VMware Engine**: Security for VMware workloads.
*   **NSX-T**: Micro-segmentation, distributed firewall.
*   **Integration**: Cloud Armor, VPC firewalls for north-south traffic.
