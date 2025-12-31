# Enterprise Application Blueprint - Architecture

## Overview
Blueprint for deploying an enterprise developer platform on Google Cloud, built on top of the **Enterprise Foundation Blueprint**.

## Key Architectural Decisions

### Deployment Archetype
*   **Multi-Region**: Deploy across multiple regions for availability during regional outages.

### Organizational Architecture
*   **Foundation Integration**: Deploys on top of Enterprise Foundation Blueprint.
*   **Three Environments**: Development, Nonproduction, Production (from foundation).
*   **Isolation**: Separate projects and access controls per environment.

### Developer Platform Cluster Architecture
*   **Container-Based**: Package and deploy apps as containers on **GKE**.
*   **Active-Active**: Replicate containers across regions for high availability and rapid rollouts.
*   **Production**: 2 GKE clusters in 2 different regions.
*   **Nonproduction**: 2 GKE clusters in 2 regions (for staging cross-regional settings).
*   **Development**: 1 GKE cluster (cost savings).
*   **High Availability Control Planes**: For each GKE cluster.

### GKE Cluster Configuration
*   **Private IP**: Private Service Connect for control plane access; private node pools.
*   **Access via Connect Gateway**: Unified credentials for multi-cluster access.
*   **Cloud NAT**: Pods access public resources without direct internet exposure.
*   **Container-Optimized OS**: Limit attack surface.
*   **Shielded GKE Nodes**: Enhanced security.
*   **Fleet Management**: Group GKE clusters per environment for unified management.

### Networking & Security
*   **Sameness Across Clusters**: Kubernetes objects with same name treated as same entity across clusters.
*   **IAM & RBAC**: Groups and third-party identity providers for cluster access.
