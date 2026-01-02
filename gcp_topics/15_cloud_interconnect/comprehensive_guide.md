# Cloud Interconnect - Comprehensive Guide

## Overview
Connects on-premises network to Google Cloud VPC via **dedicated physical connections** (RFC 1918 private IP access).
- **Traffic**: Does **NOT** traverse the public Internet.
- **Latency**: Low and consistent.
- **Security**: Private (but **NOT encrypted by default** - see MACsec).

---

## Interconnect Types (Exam Critical)

| Feature | Dedicated Interconnect | Partner Interconnect |
| :--- | :--- | :--- |
| **Connection** | Direct physical cable to Google Node. | Logic connection via Service Provider (ISP/Telco). |
| **Bandwidth** | **10 Gbps** or **100 Gbps** increments. | **50 Mbps** to **50 Gbps**. |
| **Location** | You must be in a specific Google **Colocation Facility**. | You connect to a partner (Equinix, AT&T, etc.) anywhere. |
| **Capacity** | Massive scale (Scaling up). | Flexible scale (Sub-10G needs). |
| **SLA** | 99.9% or 99.99%. | 99.9% or 99.99% (between Google/Partner). |

### 1. Dedicated Interconnect
- **Use Case**: High bandwidth (>= 10 Gbps), data center is co-located with Google.
- **Equipment**: You need your own router in the Google colo facility.

### 2. Partner Interconnect
- **Use Case**: Lower bandwidth needs (e.g., 500 Mbps), or your data center is NOT in a Google colo.
- **Equipment**: Service Provider handles the physical link to Google.

---

## Peering (Not Interconnect)

### Direct Peering
- **Traffic**: Reaches Google **Public IPs** (YouTube, Search, Workspace, Public APIs).
- **Network**: Does **NOT** access VPC private IPs (without complex NAT setup).
- **SLA**: **None**.
- **Use Case**: ISP lowering transit costs to Google.

### Carrier Peering
- Same as Direct Peering but via a provider.
- **SLA**: **None**.

---

## Redundancy & SLA

### 99.9% SLA (Development/Non-Critical)
- **Dedicated**: 2 connections in **one metro** (different zones are good, but same facility is risky).

### 99.99% SLA (Production/Critical)
- **Dedicated**: 4 connections total.
  - 2 connections in Metro A (Zone 1 & 2).
  - 2 connections in Metro B (Zone 1 & 2).
- **Goal**: Survive entire metro failure.

---

## Encryption (MACsec vs VPN)

Interconnect is **unencrypted** by default (private fiber, but readable wiretap).

**How to Encrypt?**
1.  **HA VPN over Interconnect** (Standard solution):
    - Run IPsec VPN tunnels *on top* of the Interconnect attachment (VLAN).
    - **Pros**: End-to-end encryption.
    - **Cons**: Reduced throughput (IPsec overhead).
2.  **MACsec for Dedicated Interconnect**:
    - **Hardware-level** encryption (L2).
    - **Pros**: Line-rate encryption (100 Gbps).
    - **Cons**: Requires supported hardware routers on both ends.

---

## Exam Focus Areas

1.  **Choosing a Solution**:
    - "Need 200 Mbps connection, private IP". -> **Partner Interconnect**. (Dedicated min is 10G).
    - "Need 40 Gbps, massive data transfer". -> **Dedicated Interconnect** (4 x 10G links).
    - "Need access to Workspace apps, no VPC access needed, save internet bandwidth". -> **Direct Peering** (if eligible) or **Partner Interconnect** (with Google API access). Actually Interconnect is usually preferred now for APIs too via "Private Service Connect" or "Private Google Access for on-prem".

2.  **Backup Strategy**:
    - "Primary is 10G Interconnect. What is the cheapest backup?"
    - **Cloud VPN**. (Bandwidth might be lower, but it works as failover).
    - "Primary is 10G Interconnect. Backup must handle full load."
    - **Redundant Interconnect** (VPN cannot match 10G easily without many tunnels).

3.  **Security**:
    - "Compliance requires encryption in transit, but we have Interconnect".
    - Solution: **HA VPN over Interconnect**.
