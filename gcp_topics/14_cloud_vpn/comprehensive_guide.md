# Cloud VPN - Comprehensive Guide

## Overview
Connects on-premises network to Google Cloud VPC via **IPsec VPN** tunnels over the public Internet.
- **Protocol**: IPsec (IKEv1/IKEv2).
- **Encryption**: Encrypted in transit (AES-128/256).
- **Cost**: Low (Internet egress + hourly tunnel fee).
- **Setup Time**: Fast (Minutes).

---

## Types of Cloud VPN

### 1. HA VPN (High Availability) - Recommended
- **SLA**: **99.99%** (if configured correctly).
- **Topology**:
  - **Active/Active**: Both tunnels carry traffic (ECMP).
  - **Active/Passive**: One tunnel carries traffic, other is standby.
- **Requirement**:
  - Must use **BGP** (Dynamic Routing) via Cloud Router.
  - Must connect **two interfaces** to redundant peer gateways (or two interfaces on one peer gateway).
- **Capacity**: Approx 3 Gbps per tunnel. High throughput requires multiple tunnels.

### 2. Classic VPN (Legacy)
- **SLA**: 99.9%.
- **Routing**: Supports BGP or **Static Routes**.
- **Use Case**: Connecting to legacy devices that don't support BGP.
- **Deprecation**: Do not use for new deployments.

---

## Routing & Cloud Router
Both HA VPN and Interconnect rely on **Cloud Router** for dynamic routing.
- **Cloud Router**: A fully distributed, managed Google service (not a single bottleneck/VM).
- **BGP**: Exchanges routes between VPC and On-prem.
- **Global Dynamic Routing**:
  - If VPC mode is **Regional**: Cloud Router only learns/advertises routes in its own region.
  - If VPC mode is **Global**: Cloud Router learns/advertises routes for **all subnets** in the VPC (globally).

---

## Exam Focus Areas

1.  **HA VPN SLA**:
    - Scenario: "Need 99.99% availability for VPN".
    - Solution: **HA VPN** with 2 tunnels connected to redundant peer interfaces.

2.  **Routing**:
    - Scenario: "On-prem added a new subnet, but GCP can't see it". (Using Static Routing).
    - Solution: Switch to **Dynamic Routing (BGP)** so routes propagate automatically.

3.  **VPN vs Interconnect**:
    - Scenario: "Need 2 Gbps bandwidth, quick setup". -> **Cloud VPN** (Cheaper, fast).
    - Scenario: "Need 20 Gbps bandwidth". -> **Dedicated Interconnect** (VPN caps out around 3Gbps/tunnel, managing 6+ tunnels is complex).

4.  **MTU**:
    - Cloud VPN MTU is **1460 bytes**.
    - If on-prem sets MTU to 1500 and creates fragments -> VPN drops fragments -> Connectivity issues (SSH hangs).
    - **Fix**: Clamp MSS at router or lower MTU on servers.
