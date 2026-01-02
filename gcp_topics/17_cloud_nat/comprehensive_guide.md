# Cloud NAT - Comprehensive Guide

## Overview
**Network Address Translation (NAT)** service that allows **private** instances (no External IP) to access the Internet.
- **Outbound Only**: Allows outgoing connections and established responses. Does **not** allow unsolicited inbound connections.
- **Managed Service**: Not a proxy VM. High availability by design.
- **Regional**: You create a NAT Gateway in a specific region for a specific Cloud Router.

---

## Types of Cloud NAT

### 1. Public NAT
- **Use Case**: Allow private VMs (e.g., Database servers, App servers) to download patches/packages from the Internet.
- **Security**: Prevents VMs from being directly exposed to the Internet (no external IP listening).
- **Configuration**:
  - **Manual Allocation**: You reserve Static IPs for the NAT Gateway (good for allowlisting on target firewalls).
  - **Auto Allocation**: Google assigns IPs automatically.

### 2. Private NAT
- **Use Case**: Inter-VPC communication where **IP ranges overlap**.
- **Mechanism**: Translates source IP to a non-overlapping range before sending to peer.
- **Hybrid NAT**: NAT traffic to on-prem over VPN/Interconnect.

---

## Logging & Monitoring
- **NAT Logs**: Captures translation events. Important for auditing "Who accessed this malicious IP?".
- **Metrics**:
  - **Open connections**: Track usage.
  - **Error: Out of resources**: Indicates **Source Port Exhaustion**.
  - **Dropped packets**: Rate limit hit.

---

## Exam Focus Areas

1.  **Port Exhaustion**:
    - **Concept**: Each External IP has 64k ports. If you have many VMs making many connections, you run out.
    - **Fix 1**: Increase **minimum ports per VM** (if you have few VMs).
    - **Fix 2**: Add more **External IPs** to the NAT Gateway (linear scale).

2.  **Private Google Access vs Cloud NAT**:
    - **Scenario**: "Private VM needs to reach Cloud Storage".
    - Answer: **Private Google Access** (internal route, cheaper/faster).
    - **Scenario**: "Private VM needs to reach `github.com`".
    - Answer: **Cloud NAT**.

3.  **No Inbound Access**:
    - **Scenario**: "You enabled Cloud NAT but cannot SSH into the VM from home".
    - Reason: NAT is **outbound only**. Use **IAP (Identity-Aware Proxy)** for inbound SSH.
