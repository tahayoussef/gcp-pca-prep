# Palo Alto VM-Series NGFW on Google Cloud

Deploying third-party Next-Generation Firewalls (NGFW) like Palo Alto VM-Series allows you to extend existing enterprise security policies to the cloud.

## Architecture
The VM-Series runs on **Compute Engine** and requires multiple network interfaces (NICs) to separate traffic planes:
1.  **Management Interface**: Used for administrative access (UI/CLI).
2.  **Untrust Interface**: The "exterior" gateway. Handles traffic to/from the internet or other untrusted networks.
3.  **Trust Interface**: The "internal" gateway. Connected to the private VPC networks containing protected workloads.

## Key Deployment Concepts
-   **Management Interface Swap**: A required configuration step that makes the **Untrust** interface the primary NIC. This is necessary for the firewall to correctly receive traffic from Google Cloud External Load Balancers.
-   **High Availability & Scaling**: 
    -   Deploy firewalls in a **Managed Instance Group (MIG)** for resiliency.
    -   Use **Internal TCP/UDP Load Balancers** as the "next hop" in VPC routes for the Trust network to ensure HA.
-   **Panorama**: A centralized management appliance (can run on-premises or on GCP) used to manage multiple VM-Series firewalls as a single entity.
-   **Hub-and-Spoke**: Common topology where the firewall resides in a Hub VPC, providing transitive inspection for multiple Spoke VPCs via VPC Peering or VPN.
