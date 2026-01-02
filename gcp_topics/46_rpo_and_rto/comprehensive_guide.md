# RPO and RTO - Comprehensive Guide

## Overview
**Recovery Point Objective (RPO)** and **Recovery Time Objective (RTO)** are the two most critical metrics in Disaster Recovery (DR) planning. They define the business's tolerance for data loss and downtime.

## Definitions

### Recovery Point Objective (RPO)
- **Definition**: The maximum acceptable amount of data loss measured in time.
- **Question**: "How much data can we afford to lose?"
- **Determined by**: Backup frequency and data replication lag.
- **Example**: An RPO of 1 hour means you might lose up to 1 hour of data. You need backups at least every hour.

### Recovery Time Objective (RTO)
- **Definition**: The maximum acceptable duration of downtime before services are restored.
- **Question**: "How quickly must we be back online?"
- **Determined by**: failover process speed (automated vs manual), startup time, and data hydration.
- **Example**: An RTO of 4 hours means the system must be up within 4 hours of a disaster.

---

## DR Patterns & Trade-offs

| Pattern | RPO | RTO | Cost | Description |
| :--- | :--- | :--- | :--- | :--- |
| **Cold DR** | High (Hours/Days) | High (Hours/Days) | Lowest | Backups only. Infrastructure is provisioned only after disaster strikes. |
| **Warm DR** | Medium (Minutes/Hours) | Medium (Minutes/Hours) | Medium | **Passive standby**. Database is replicating (low RPO), but compute is minimal/stopped and scaled up on failover. |
| **Hot DR** | Low (Seconds/Zero) | Low (Seconds/Zero) | Highest | **Active-Active** or **Active-Passive (Hot Standby)**. Fully redundant infrastructure running in parallel. Immediate failover. |

## Exam Focus Areas

1.  **Cost Optimization**:
    - "Minimize cost for a non-critical internal app." -> **Cold DR** (Restore from backup).
    - "Critical banking transaction system." -> **Hot HA/DR** (Spanner Multi-region, Load Balancer).

2.  **RPO Limitations**:
    - If RPO is 10 minutes, a nightly backup is **insufficient**. You need frequent transaction log backups or synchronous replication.

3.  **RTO Reduction**:
    - To lower RTO, use **Infrastructure as Code** (Terraform) or **Managed Instance Groups** (auto-healing/scaling) to speed up recovery.
    - **Cloud DNS** failover is faster than DNS propagation but check TTL settings.
