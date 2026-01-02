# Cloud VPC - Comprehensive Guide

## VPC Fundamentals

### Overview
Virtual Private Cloud (VPC) is a global, software-defined network for your GCP resources.
- **Global**: A single VPC can span all GCP regions (unlike AWS where VPC is regional).
- **Subnets**: Regional. Defined by IP ranges (CIDR).
- **Resources**: VMs (Compute Engine), GKE clusters, App Engine Flex, etc. live in subnets.

### VPC Modes
1.  **Auto Mode**:
    - Automatically creates a subnet in **every region** with a predefined IP range (`10.128.0.0/9` block).
    - **Pros**: Quick start.
    - **Cons**: Hard to manage IP overlap with on-prem or peered networks. **Avoid in Production**.
2.  **Custom Mode**:
    - No subnets at creation. You manually create subnets in specific regions.
    - **Pros**: Full control over IP ranges (prevents overlap). **Recommended for Production**.

---

## Connectivity & Sharing

### 1. VPC Peering
Connects two VPCs directly (same or different organization).
- **Performance**: Internal IP connectivity, low latency, no gateway bottleneck.
- **Constraints**:
  - **NON-TRANSITIVE**: If A peers with B, and B peers with C, **A cannot talk to C**.
  - **CIDR Overlap**: Cannot peer if IP ranges overlap.
- **Route Exchange**: Can export/import custom routes (e.g., to share a VPN connection from a transit VPC).

### 2. Shared VPC
Allows centralized network administration while delegating instance creation.
- **Host Project**: Owns the VPC network, subnets, and firewall rules. Managed by **Shared VPC Admin**.
- **Service Project**: Attached to Host Project. Users can launch VMs into the Host's subnets.
- **Roles**:
  - **Shared VPC Admin**: Manages network (host project).
  - **Service Project Admin**: Manages VMs (service project), uses shared subnets.
- **Use Case**: Centralize networking/security, decentralized app teams.

---

## Private Access Options (Exam Critical)

| Feature | Use Case | Implementation |
| :--- | :--- | :--- |
| **Private Google Access (PGA)** | VMs with **no external IP** need to access Google APIs (GCS, BigQuery). | Enabled at **Subnet** level. Routes traffic to Google APIs internally. |
| **Private Services Access (PSA)** | Access **Google Managed Services** (Cloud SQL, Memorystore) via private IP. | Uses **VPC Peering** (behind the scenes) to Google's tenant project. Requires reserved IP range. |
| **Private Service Connect (PSC)** | Access services (Google, 3rd party, or your own) in another VPC via a **private Endpoint IP**. | No Peering required. Unidirectional. Avoids CIDR overlap issues. |
| **Serverless VPC Access** | Cloud Run/App Engine/Functions need to access VPC resources (VMs, Cloud SQL). | Connector VMs or Direct VPC Egress. |

---

## IP Addressing
- **Internal IP**: RFC 1918 (10.x.x.x, 172.16.x.x, 192.168.x.x).
- **External IP**: Ephemeral (changes on stop/start) or Static (reserved).
- **Alias IP**: Additional internal IP ranges assigned to a VM (useful for containers/pods).
- **BYOIP**: Bring your own public IP addresses to Google.

---

## Flow Logs
- **VPC Flow Logs**: Captures sample of network flows (5-tuple) for analysis.
- **Use Case**: Forensics, real-time security analysis, expense optimization.
- **Storage**: Sent to Cloud Logging (and then BigQuery for analysis).

---

## Exam Focus Areas

1.  **VPC Peering Limits**:
    - **Scenario**: "VPC A needs to talk to VPC C, but they are both peered to Hub VPC B". -> **Peering is Non-Transitive**. You must peer A directly to C (mesh) or use a Proxy/VPN Gateway in B (complex).

2.  **Shared VPC vs Peering**:
    - **Scenario**: "Organization wants centralized network control but separate billing/projects for app teams". -> **Shared VPC**.
    - **Scenario**: "Two autonomous organizations need to connect". -> **VPC Peering**.

3.  **Accessing APIs securely**:
    - **Scenario**: "Security policy forbids External IPs. App needs to read from Cloud Storage". -> Enable **Private Google Access** on the subnet.

4.  **Hybrid Connectivity**:
    - **Scenario**: "Connect on-prem to multiple VPCs".
    - Solution: Connect on-prem to **Hub VPC** (via VPN/Interconnect). Peer Spoke VPCs to Hub. Enable **Export Custom Routes** on Hub peering.
