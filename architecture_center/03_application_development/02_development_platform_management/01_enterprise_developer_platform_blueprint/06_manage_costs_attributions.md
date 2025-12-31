# Manage Costs and Attributions

## Overview
Cost management and attribution strategy for the multi-tenant developer platform.

## Proactive Cost Planning
*   **Budget Alerts**: Set budgets on projects for cost tracking.
*   **Cost Attribution Granularity**:
    *   **Project Costs**: Single-tenant projects attributed via metadata labels in billing exports.
    *   **Multi-Tenant Cluster Costs**: GKE cost allocation provides namespace/label-level breakdown.
    *   **Shared Costs**: Shared resources (platform infrastructure) allocated to IT cost center or split proportionally.

## Cost Attribution by Project Type
*   **Platform Projects** (shared): infra-cicd, app-factory, logging → Shared costs.
*   **GKE Clusters** (multi-tenant): GKE VMs, disks → Multi-tenant cluster costs.
*   **Network/Logging** (shared): Load balancers, monitoring → Shared costs.
*   **Application Projects** (single-tenant): CI/CD, AlloyDB → Project costs (attributable to specific tenant).

## Continuous Resource Monitoring
*   **Cloud Monitoring**: Track GKE cluster utilization; identify underutilized resources.
*   **BigQuery Billing Exports**: Detailed cost analysis and reporting.

## Optimization Techniques
*   Apply cost-optimization techniques after establishing baseline (see GKE cost optimization best practices).
