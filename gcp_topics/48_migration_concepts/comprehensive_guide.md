# Migration Concepts - Comprehensive Guide

## Overview
Migration to Google Cloud follows a structured framework to ensure success. The PCA exam focuses on selecting the right phase, strategy, and tool for a given scenario.

## The 4 Phases of Migration
1.  **Assess**: Discovery of existing environment. Identify apps, dependencies, resources. (Tool: StratoZone, Migration Center).
2.  **Plan**: Define strategy (6 Rs), landing zone design, governance, identity.
3.  **Deploy**: Execute the migration (Lift & Shift, etc.). (Tool: Migrate to VMs, DMS).
4.  **Optimize**: Post-migration. Rightsizing, modernizing to managed services, cost optimization.

## The "6 Rs" Migration Strategies

| Strategy | Description | GCP Example | Pros/Cons |
| :--- | :--- | :--- | :--- |
| **Rehost** (Lift & Shift) | Move "as-is" with minimal changes. | VM on-prem -> **Compute Engine**. | Fastest, lowest risk / No cloud-native benefits. |
| **Replatform** (Lift & Optimize) | Minor optimizations (OS, DB) but core app stays same. | Self-managed MySQL -> **Cloud SQL**. | Balance of speed and benefit. |
| **Refactor** (Move & Improve) | Re-architect / rewrite code to be cloud-native. | Monolith -> **Microservices (GKE/Cloud Run)**. | Highest long-term value / High effort & cost. |
| **Repurchase** | Replace with SaaS or different product. | Exchange Server -> **Google Workspace**. | Simple / Loss of customization. |
| **Retire** | Turn off unneeded systems. | Decomissioning legacy app. | Cost saving. |
| **Retain** | Keep on-prem (for now). | Mainframe, Regulation. | N/A. |

## Migration Tools Decision Tree

1.  **Moving entire VM (OS + App)?** -> **Migrate to Virtual Machines**.
    - *Features*: Rightsizing recommendations, Test clones, specific replication.
2.  **Moving Database?** -> **Database Migration Service (DMS)**.
    - *Targets*: Cloud SQL (MySQL, PostgreSQL, SQL Server), AlloyDB.
    - *Homogeneous*: Free.
    - *Heterogeneous*: Paid (managed conversion).
    - *Oracle*: Bare Metal Solution or BMS toolkit.
3.  **Moving massive data (Offline)?** -> **Transfer Appliance**.
4.  **Moving Data (Online/Object)?** -> **Storage Transfer Service**.
