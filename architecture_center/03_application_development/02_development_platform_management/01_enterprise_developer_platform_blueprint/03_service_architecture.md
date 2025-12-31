# Service Architecture

## Overview
How services are deployed, exposed, and managed within the Enterprise Developer Platform on GKE.

## Namespaces
*   **Organization**: Group services by purpose (frontend, backend, etc.).
*   **Isolation**: Each namespace has its own resources (pods, services, deployments).

## Service Exposure
*   **GKE Gateway Controller**: Exposes services to internet via Cloud Load Balancing.
*   **Multi-Cluster, Multi-Region**: Load balancer config spans multiple clusters/regions.
*   **Anycast IP**: Google's network infrastructure provides low-latency access.
*   **HTTPS Only**: HTTP requests redirected to HTTPS.
*   **Certificate Manager**: Manages public TLS certificates.
*   **Protection**: Cloud Armor (DDoS protection) and Cloud CDN (content delivery).

## Cloud Service Mesh
*   **mTLS**: Mutual TLS for authentication and encryption between services.
*   **CA Service**: Issues TLS certificates.
*   **Service-to-Service Auth**: Only authorized clients can access services.

## Distributed Services
*   **Multi-Cluster Abstraction**: Service runs in same namespace across multiple clusters.
*   **High Availability**: Service remains available if one cluster fails.
*   **Cross-Region Routing**: Traffic routed to another region only during regional failure.

## Service Identity
*   **Workload Identity Federation**: Kubernetes service account acts as Google Cloud service account.
*   **Common Identity**: Each distributed service instance within environment has common identity.
*   **Minimal Permissions**: Services have only necessary permissions.
