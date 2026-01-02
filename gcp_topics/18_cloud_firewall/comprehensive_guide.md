# Cloud Firewall - Comprehensive Guide

## Overview
Distributed, stateful firewall service enforced at the **VM instance level** (hypervisor).
- **Stateful**: If you allow outbound connection, the return traffic is automatically allowed.
- **Direction**: **Ingress** (Incoming) and **Egress** (Outgoing).
- **Implied Rules**:
  - **Deny All Ingress** (by default).
  - **Allow All Egress** (by default).

---

## VPC Firewall Rules (Project Level)
Standard rules defined within a VPC network.
- **Components**:
  - **Priority**: 0 (High) to 65535 (Low). Default 1000. Use integers.
  - **Action**: Allow or Deny.
  - **Target**: All instances, **Target Tags** (legacy), or **Service Accounts** (Recommended).
  - **Source/Dest**: IP ranges (CIDR), Source Tags, Source Service Accounts.

**Identity-Based Rules**:
- Instead of IP ranges, use **Service Accounts**.
- Example: "Allow `frontend-sa` to access `backend-sa` on Port 80".
- **Benefit**: Auto-scales with instance creation; no IP management needed.

---

## Hierarchical Firewall Policies (Org/Folder Level)
Manage firewall rules at the **Organization** or **Folder** level to enforce compliance across all projects.

**Key features**:
- **Consistency**: Enforce "Block SSH globally" or "Allow Corporate VPN globally".
- **Delegation (`goto_next`)**:
  - This action in a higher-level policy (Org) passes evaluation to lower-level policies (Folder/Project).
  - Allows "Centralized guardrails, decentralized application rules".
- **Evaluation Order**:
  1.  Organization Policy.
  2.  Folder Policy.
  3.  VPC Firewall Rules (Project).

---

## Exam Focus Areas

1.  **Service Accounts vs Tags**:
    - **Scenario**: "Strict security, dynamic environment". -> **Service Accounts**. (Tags are mutable strings users can edit; SAs are strictly IAM controlled).

2.  **Hierarchical Policies**:
    - **Scenario**: "Security team wants to block port 22 on ALL projects, but App Admins manage their own allow rules".
    - Answer: Create **Organization Firewall Policy** with a **Deny** rule on Port 22 (Priority 100).

3.  **Troubleshooting**:
    - **Scenario**: "Rule allows 0.0.0.0/0 on port 80, but traffic fails".
    - Check **Priority** (Higher priority deny?).
    - Check **Network Tags** (Is the VM tagged?).
    - Check **OS Firewall** (iptables on the VM itself?).

4.  **Logging**:
    - **Firewall Rules Logging**: Can be enabled per rule. Logs "Allow" or "Deny" events to Cloud Logging.
