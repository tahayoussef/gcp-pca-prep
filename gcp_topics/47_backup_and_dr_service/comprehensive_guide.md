# Backup and DR Service - Comprehensive Guide

## Overview
**Google Cloud Backup and DR Service** (formerly Actifio) is a centrally managed solution for protecting workloads across Google Cloud (Compute Engine, GKE, VMware Engine) and hybrid environments.

## Key Features
- **Centralized Management**: Single console to manage backups for varied workloads (VMs, Databases).
- **Application Aware**: Aware of databases (Oracle, SQL Server, SAP HANA) to ensure consistency.
- **Incremental Forever**: Uses Google Cloud PD snapshots efficiently but manages them with long-term retention policies.
- **Backup Vaults**: Immutable storage for backups to protect against ransomware and accidental deletion.

## Backup & DR Service vs. Standard Snapshots

| Feature | Standard PD Snapshots | Backup and DR Service |
| :--- | :--- | :--- |
| **Management** | Individual/Scripted or Snapshot Schedules | Centralized Policy-based Management |
| **Retention** | Limited visibility, manual cleanup | Long-term retention, GFS (Grandfather-Father-Son) rotation |
| **Consistency** | Crash consistent (unless scripts used) | **Application consistent** (DB aware) |
| **Storage** | Regional (usually) | Multi-regional, Independent from source |
| **Ransomware** | Mutable (unless locked) | **Immutable** Backup Vaults |

## Usage Scenarios
1.  **Compliance**: "Need to retain daily backups for 7 years." -> Use Backup & DR Service policies.
2.  **Database Protection**: "Need application-consistent backups for a SQL Server on Compute Engine." -> Backup & DR agent ensures consistency.
3.  **Ransomware Protection**: "Protect backups from admin deletion." -> Backup Vaults (Immutable).
4.  **VMware Engine**: Native integration to backup GCVE VMs.

## Exam Decision Tree
- **Simple VM protection, short retention?** -> **Snapshot Schedules**.
- **Complex Enterprise, DBs, Long-term Compliance, Central Management?** -> **Backup and DR Service**.
- **Managed DB Service (Cloud SQL)?** -> **Automated Backups** (Built-in feature).
