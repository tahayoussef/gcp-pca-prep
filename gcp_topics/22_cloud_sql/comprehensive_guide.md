# Cloud SQL - Comprehensive Guide

## Overview
Fully managed relational database service for **MySQL**, **PostgreSQL**, and **SQL Server**.
- **Use Case**: General purpose OLTP (Online Transaction Processing). ERP, CRM, E-commerce, CMS.
- **Scaling Limit**: Vertically scale up to ~128 vCPUs / 64TB storage. If you need more writes, move to Spanner.

---

## High Availability (HA)
- **Regional HA**: Primary instance in Zone A, Standby instance in Zone B.
- **Mechanism**: **Synchronous replication** of Persistent Disks.
- **Failover**: Automatic. If Zone A fails, Standby in Zone B becomes Primary. Processing stops for ~60s (DNS switch).
- **Cost**: Doubles the instance and storage cost (2 VMs running).

---

## Read Replicas (Scaling Reads)
- **Horizontal Scaling**: Create up to 10 Read Replicas.
- **Mechanism**: **Asynchronous replication**. (Lag is possible).
- **Zones**: Can be in same zone, different zone, or different region (Cross-Region Replica).
- **Promotion**: A Read Replica can be promoted to a standalone primary (useful for Migration or DR testing).

---

## Maintenance & Backups
- **Maintenance Windows**: Required downtime (approx 60s) for updates. You define the window (e.g., Sunday 02:00 AM).
- **Automated Backups**: Daily. Stored for 7 days (configurable).
- **Point-in-Time Recovery (PITR)**: Restore database to specific timestamp (uses Write-Ahead Logs).

---

## Editions (New Tier)
- **Standard**: Good for Dev/Test.
- **Enterprise**: Standard production.
- **Enterprise Plus**:
  - Better machine types (CAS).
  - **Data Cache**: Flash-optimized read cache.
  - **99.99% SLA**.

---

## Exam Focus Areas

1.  **Scaling**:
    - **Scenario**: "Database CPU high due to read queries".
    - Solution: **Add Read Replicas**, redirect read traffic.
    - **Scenario**: "Database CPU high due to write queries".
    - Solution: **Vertical Scale UP** (increase instance size). If maxed out -> **Spanner**.

2.  **Migration**:
    - **Scenario**: "Migrate on-prem MySQL to Cloud SQL with min downtime".
    - Solution: **Database Migration Service (DMS)**. Sets up replication.

3.  **Connection**:
    - **Cloud SQL Auth Proxy**: Recommended secure way to connect without IP allowlisting. Handles authentication (IAM).
    - **Private Service Connect**: Modern way to expose SQL inside VPC.
