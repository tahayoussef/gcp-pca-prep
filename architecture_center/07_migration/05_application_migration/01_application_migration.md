# Application Migration

## Migrate Containers to GKE
*   **From Other Kubernetes**: Export manifests, ConfigMaps, Secrets; import to GKE.
*   **From Docker Swarm/Mesos**: Convert to Kubernetes manifests.
*   **Tooling**: Migrate for Anthos to discover and migrate containerized apps.

## Migrate Across Google Cloud Regions

### Reasons
*   Proximity to users (reduce latency).
*   Disaster recovery.
*   Regulatory compliance (data residency).

### Design Resilient Single-Region Environments
Before multi-region migration, ensure single-region resilience:
*   **Multi-Zone**: Deploy across zones for HA.
*   **Backups**: Regular snapshots, exports.

### Architect Workloads for Multi-Region
*   **Stateless Apps**: Easy to replicate; use global load balancer.
*   **Stateful Apps**: Database replication (Cloud Spanner for global, Cloud SQL cross-region replicas).
*   **Storage**: Multi-region Cloud Storage buckets.

### Prepare Data and Batch Workloads
*   **Data Replication**: Use Cloud SQL replication, Bigtable replication, or Datastream.
*   **Batch Jobs**: Ensure idempotency; run in multiple regions.

### Migration Steps
1. Set up target region infrastructure.
2. Replicate data to target region.
3. Deploy applications to target region.
4. Test thoroughly.
5. Update load balancer to route traffic to new region.
6. Decommission old region resources (after validation).
