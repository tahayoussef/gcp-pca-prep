# Logging and Monitoring

## Overview
Centralized logging and monitoring strategy for the Enterprise Developer Platform.

## Logging Storage
*   **Central Log Buckets**: Cloud Logging stores system and application logs.
*   **Per-Environment Logging Projects**: Each environment has dedicated logging project.
*   **Granular Access**: Logs separated by tenant and type (e.g., frontend logs, backend logs).
*   **Log Types**:
    *   Platform infrastructure logs (multi-tenant)
    *   Application factory logs
    *   Node, cluster control plane, non-tenant logs (by environment)
    *   Tenant container/pod logs (by environment and tenant)
    *   Application build/deploy logs (by tenant)

## Application Monitoring
*   **GKE Dashboards**: Predefined dashboards for GKE observability.
*   **Google Cloud Managed Service for Prometheus**: Collects Prometheus metrics globally; query with PromQL.
*   **Grafana**: Use with Prometheus data.
*   **Cloud Service Mesh Dashboards**: Observe and troubleshoot service interactions.
*   **Multi-Project Metrics Scope**: Unified monitoring across projects.

## Threat & Vulnerability Monitoring
*   **Security Command Center Premium**: Container Threat Detection for GKE workloads.
*   **Web Security Scanner**: Detects vulnerabilities in internet-facing services.
