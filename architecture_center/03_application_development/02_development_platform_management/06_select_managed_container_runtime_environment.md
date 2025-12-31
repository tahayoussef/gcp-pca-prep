# Select a Managed Container Runtime Environment

## Overview
Decision guide for choosing between **Cloud Run** and **GKE Autopilot** for managed container workloads.

## Cloud Run
*   **Serverless**: Fully managed, scales to zero.
*   **Best For**: Stateless HTTP services, event-driven workloads, simple deployments.
*   **Limitations**: No persistent storage, limited to HTTP/gRPC, 60-minute request timeout.

## GKE Autopilot
*   **Managed Kubernetes**: Google manages nodes, scaling, security patching.
*   **Best For**: Complex microservices, stateful apps, need Kubernetes APIs, custom networking.
*   **Flexibility**: Full Kubernetes features (DaemonSets, StatefulSets, custom controllers).

## Selection Criteria

### Choose Cloud Run if:
*   Simple HTTP/gRPC services
*   Scale-to-zero needed
*   Minimal operations overhead
*   Short-lived requests

### Choose GKE Autopilot if:
*   Need Kubernetes ecosystem (Helm, operators, etc.)
*   Stateful workloads (databases, caches)
*   Complex networking requirements
*   Job/batch processing with Kubernetes Jobs

## Migration
*   Both support standard containers; relatively easy to migrate between them if needed.
