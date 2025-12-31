# Decide the Network Design

## Overview
Designing a network for your landing zone involves choosing a VPC topology that balances isolation, scale, and centralized management. The choice impacts how you manage connectivity, security/firewalls, and routing.

## Network Design Options

### Option 1: Shared VPC (Recommended)
A **Shared VPC** per environment (e.g., one for Prod, one for Dev).
*   **Architecture**: A Host Project manages the network (subnets, routes, firewalls), while Service Projects (workloads) attach to it.
*   **Pros**: Centralized control of IP space and security; separation of network ownership from application ownership.
*   **Connectivity**: Environments are isolated by default; use Hybrid Connectivity (Interconnect/VPN) to connect back to on-prem.

### Option 2: Hub-and-Spoke with Centralized Appliances
A **Hub** VPC handles north-south traffic and connects to **Spoke** VPCs via Peering.
*   **Architecture**: Appliance VMs (NGFWs) in the Hub inspect traffic.
*   **Pros**: Enables Layer 7 inspection and centralized appliance vendor management.
*   **Cons**: Higher complexity, possible bandwidth bottlenecks at the appliance.

### Option 3: Hub-and-Spoke without Appliances
Similar to Option 2 but without central inspection appliances.
*   **Architecture**: Hub handles hybrid connectivity; Spokes peer with the Hub.
*   **Pros**: Autonomy for spoke teams.
*   **Cons**: No transitivity (Spoke A cannot talk to Spoke B via Hub); harder to manage central policies.

### Option 4: Private Service Connect (Consumer-Producer)
Expose specific services via **Private Service Connect (PSC)** endpoints.
*   **Architecture**: Producer VPC publishes a service; Consumer VPC accesses it via a local IP.
*   **Pros**: Maximum isolation; no peering dependencies; solves overlapping IP issues.
*   **Use Case**: SaaS-like internal services, multi-tenant architectures.

## Key Considerations
*   **Isolation**: Do Dev and Prod need to speak? (Usually No).
*   **Inspection**: Do you need Deep Packet Inspection (DPI/Layer 7)?
*   **Scale**: Be aware of Quotas for Peering groups and Forwarding Rules.
