# Hybrid/Multicloud Secure Networking Patterns

## Mirrored Pattern
Identical network topology replicated across environments. **Use**: Consistent security posture; simplified management.

## Meshed Pattern
Full mesh connectivity between all environments. **Use**: Any-to-any communication; complex but flexible.

## Gated Patterns
Centralized control points (gateways) for traffic between environments.

### Gated Egress
On-prem → Cloud traffic via gateway (e.g., NAT gateway, proxy). **Use**: Centralize outbound control.

### Gated Ingress
Cloud → On-prem traffic via gateway. **Use**: Centralize inbound security.

### Gated Egress & Ingress
Both directions via gateways. **Use**: Maximum control over cross-environment traffic.

## Handover Pattern
Traffic handed off between security zones (e.g., Google Cloud Load Balancer hands off to on-prem load balancer).

## Best Practices
*   Use VPC Service Controls for data perimeters
*   Implement least-privilege firewall rules
*   Monitor cross-environment traffic
*   Encrypt all traffic in transit
