# Implement Network Design

## Overview
Implementing the network design involves configuring the Virtual Private Cloud (VPC) resources and applying policies to enforce security and connectivity standards. This summary focuses on best practices for limiting exposure and configuring firewalls.

## Limiting External Access
Use **Organization Policies** to restrict direct internet access and enforce private connectivity.

### Key Constraints to Apply
1.  **Restrict Protocol Forwarding**: Prevent creation of forwarding rules with external IP addresses (`compute.restrictProtocolForwardingCreationForTypes` = `EXTERNAL`).
2.  **Define Allowed External IPs**: Prevent VM instances from being assigned external IP addresses (`compute.vmExternalIpAccess`), or allow it only for specific allowed VMs.
3.  **Disable VPC External IPv6 Usage**: Prevent external IPv6 ranges.
4.  **Skip Default Network Creation**: Disable the automatic creation of the "default" VPC in new projects to ensure all networks are intentionally designed (`compute.skipDefaultNetworkCreation`).

## Designing Firewall Rules
Firewall rules control traffic to and from VMs.

### Hierarchical Firewall Policies
Apply consistent rules across the Organization or Folders.
*   **Centralized Control**: Enforce broad rules (e.g., "Deny SSH from Internet") that apply to all projects.

### Standard Allow Rules
Common infrastructure requirements often permitted globally or at a high level:
*   **Identity-Aware Proxy (IAP)**: Allow ingress from `35.235.240.0/20` (TCP 22, 3389) for secure remote access without public IPs.
*   **Load Balancer Health Checks**: Allow ingress from Google's health check ranges (e.g., `35.191.0.0/16`, `130.211.0.0/22`).

### Best Practices
*   **Least Privilege**: Block all traffic by default.
*   **Logging**: Enable firewall rule logging for visibility.
*   **Prioritization**: Use a strict numbering scheme (e.g., specific rules > 1000, broad rules < 1000) to ensure critical rules aren't overridden.
