# Globally Distributed Apps with GKE Gateway and Cloud Service Mesh

## Overview
Multi-cluster, multi-region architecture using **GKE Gateway** and **Cloud Service Mesh** for globally distributed applications.

## Architecture
*   **Multiple GKE Clusters**: Deployed across multiple regions for global reach.
*   **Cloud Ingress**: Single global **Application Load Balancer** (anycast IP) routes to nearest healthy cluster.
*   **Mesh Ingress**: Service mesh routes traffic within and across clusters.
*   **Fleets**: Clusters grouped into fleets for unified management.

## Key Features
*   **Global Load Balancing**: Traffic routed to nearest region for low latency.
*   **Multi-Cluster Services**: Service abstraction spans multiple clusters (distributed service).
*   **Cross-Region Failover**: Automatic failover if a region becomes unavailable.
*   **mTLS**: End-to-end encryption via Cloud Service Mesh.

## Design Considerations
*   **Security**: Private clusters, mTLS, Binary Authorization.
*   **Reliability**: Multi-region deployment, health checks, circuit breakers.
*   **Performance**: Anycast IP for low-latency routing.
