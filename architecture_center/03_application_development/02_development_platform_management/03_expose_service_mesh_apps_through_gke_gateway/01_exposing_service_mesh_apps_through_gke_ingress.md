# Expose Service Mesh Apps Through GKE Gateway

## Overview
Combines **Cloud Service Mesh** with **Cloud Load Balancing** via **GKE Gateway** to expose service mesh applications to internet clients.

## Architecture
*   **Cloud Ingress**: External **Application Load Balancer** (created by GKE Gateway) routes traffic to services.
*   **Mesh Ingress Gateway**: Gateway pods within the mesh receive traffic and route to backend services using service mesh policies.

## Key Components
*   **GKE Gateway Controller**: Manages load balancer configuration.
*   **Cloud Service Mesh**: mTLS for service-to-service communication.
*   **Multi-Cluster Services (MCS)**: Enables load balancing across clusters.

## Benefits
*   **Security**: mTLS encryption, Cloud Armor DDoS protection.
*   **Observability**: Service Mesh dashboards for traffic visibility.
*   **Health Checking**: Automated health checks via load balancer.

## Use Cases
*   Exposing microservices to external clients while maintaining internal mesh security.
*   Multi-cluster deployments with global load balancing.
