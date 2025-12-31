# Expose Service Mesh Apps through GKE Gateway

## Overview
Combine **Cloud Service Mesh** with **Cloud Load Balancing** to expose service mesh applications to the internet via **GKE Gateway**.

## Architecture
*   **Cloud Ingress**: GKE Gateway creates Cloud Load Balancer with anycast IP for external access.
*   **Mesh Ingress**: Cloud Service Mesh provides mTLS, traffic management, and observability for service-to-service communication.

## Components
*   **GKE Gateway Controller**: Creates multi-cluster, multi-region load balancer.
*   **Cloud Load Balancing**: Global load distribution with HTTPS.
*   **Cloud Service Mesh**: mTLS encryption, service discovery, traffic routing.
*   **Certificate Manager**: Manages TLS certificates.
*   **Cloud Armor**: DDoS protection.
*   **Cloud CDN**: Content caching and delivery.

## Traffic Flow
1.  External request → Cloud Load Balancer (via anycast IP).
2.  Load Balancer → GKE Gateway → Mesh Ingress Gateway (in GKE cluster).
3.  Mesh Ingress → Service Mesh (mTLS encrypted) → Backend services.

## Health Checking
*   Load balancer performs health checks on mesh ingress gateway pods.
