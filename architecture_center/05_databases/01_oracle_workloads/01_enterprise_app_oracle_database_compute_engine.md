# Enterprise Application with Oracle Database on Compute Engine

## Overview
Reference architecture for running enterprise applications with **Oracle Database** on **Compute Engine** VMs.

## Architecture
*   **Application Tier**: Compute Engine VMs (web servers, application servers).
*   **Database Tier**: Oracle Database on Compute Engine VMs.
*   **Storage**: Persistent Disks (SSD/balanced) for database files.
*   **Networking**: VPC, Cloud Load Balancing.

## Key Design Considerations
*   **System Design**: Multi-tier architecture; separate VMs for app and database.
*   **Security**: Private IPs, Cloud Armor, IAM, VPC firewalls.
*   **Reliability**: Regional deployment; Oracle Data Guard for HA/DR.
*   **Cost**: Right-sized VMs; committed use discounts for predictable workloads.
*   **Performance**: Local SSDs for high-IOPS workloads; optimize instance types.
*   **Operations**: Automated backups; monitoring with Cloud Monitoring.

## HA/DR Options
*   **Oracle Data Guard**: Active-passive replication across zones/regions.
*   **Oracle RAC**: Real Application Clusters for active-active.
