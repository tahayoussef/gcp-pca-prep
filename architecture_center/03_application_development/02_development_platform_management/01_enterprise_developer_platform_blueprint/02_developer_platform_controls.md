# Developer Platform Controls

## Overview
Security and access controls for the Enterprise Developer Platform, including identity, organization structure, and networking.

## Platform Identity & Access
*   **Workload Identity Federation for GKE**: Maps Kubernetes service accounts to Google Cloud service accounts.
*   **Separate Identity Pools**: Each environment (dev/nonprod/prod) has its own identity pool to prevent cross-environment escalations.
*   **Platform Personas**: Defined roles (Platform Admin, App Developer, App Operator, etc.).

## Organization Structure
*   **Projects**: Separate projects for infrastructure, CI/CD, GKE clusters (per environment), and logging.
*   **Three Environments**: Development, Nonproduction, Production (from foundation blueprint).

## GKE Components
*   **Fleet Management**: Groups GKE clusters by environment for unified management.
*   **Cluster Configuration**: Private IPs, Container-Optimized OS, Shielded Nodes, Connect Gateway.

## Networking
*   **Private Clusters**: Private Service Connect for control plane; private node pools.
*   **Cloud NAT**: Pods access public resources without direct internet exposure.
*   **DNS**: Managed through Cloud DNS for resolution within VPC and to Google services.

## High Availability
*   **Multi-Region Deployment**: 2 GKE clusters in 2 regions for production/nonproduction.
*   **Highly Available Control Planes**: For each GKE cluster.

## Quotas & Limits
*   Platform sets quotas to prevent resource exhaustion and control costs.
