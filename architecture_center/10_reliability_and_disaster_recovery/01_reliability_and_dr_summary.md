# Reliability and Disaster Recovery

## Infrastructure Reliability Guide

### Building Blocks
*   **Redundancy**: Multi-zone, multi-region deployments.
*   **Health Checks**: Detect failures; remove unhealthy instances from load balancing.
*   **Autoscaling**: Respond to load changes automatically.

### Requirements
*   **RTO (Recovery Time Objective)**: Maximum acceptable downtime.
*   **RPO (Recovery Point Objective)**: Maximum acceptable data loss.
*   Define SLOs (Service Level Objectives) for availability, latency.

### Design
*   **High Availability**: Deploy across multiple zones in a region.
*   **Disaster Recovery**: Multi-region for resilience against regional failures.
*   **Graceful Degradation**: Continue operating with reduced functionality during partial failures.

### Traffic and Load Management
*   **Load Balancing**: Distribute traffic across healthy instances.
*   **Traffic Splitting**: Canary deployments, A/B testing.
*   **Rate Limiting**: Protect against overload.

### Manage and Monitor
*   **Cloud Monitoring**: Track SLIs, set up alerts.
*   **Error Budgets**: Define acceptable error rates; pause releases if exceeded.
*   **Chaos Engineering**: Intentionally inject failures to test resilience.

## Disaster Recovery Planning Guide

### DR Patterns (by RTO/RPO)
1.  **Cold DR (Pilot Light)**: RPO: hours/days, RTO: hours/days. Minimal infrastructure; activate on disaster.
2.  **Warm DR**: RPO: minutes/hours, RTO: minutes/hours. Partial infrastructure running; scale up on disaster.
3.  **Hot DR (Active-Passive)**: RPO: seconds/minutes, RTO: minutes. Full infrastructure standby; quick failover.
4.  **Active-Active**: RPO: near-zero, RTO: near-zero. Both regions active; instant failover.

### Building Blocks
*   **Data Replication**: Cloud SQL replicas, Cloud Spanner multi-region, Cloud Storage multi-region buckets.
*   **Snapshots**: Regular backups of persistent disks, databases.
*   **DNS Failover**: Update DNS to point to DR region.

### DR for Data
*   **Databases**: Cloud SQL cross-region replicas, Cloud Spanner automatic replication.
*   **Object Storage**: Multi-region or dual-region Cloud Storage.
*   **BigQuery**: Multi-region datasets.

### DR for Applications
*   **Stateless Apps**: Easy to replicate; deploy in multiple regions.
*   **Stateful Apps**: Require data replication; use managed databases with built-in replication.

### Locality-Restricted Workloads
*   **Challenge**: Data must stay in specific region due to regulations.
*   **Solution**: DR within same region (cross-zone); or use regional pairs that meet compliance (e.g., EU-specific regions).

### DR for Data Analytics
*   **BigQuery**: Enable multi-region for analytics datasets.
*   **Dataflow**: Deploy pipelines in multiple regions.
*   **Backup**: Export BigQuery tables to Cloud Storage; archive in different region.

## Application Availability

### Load-Balanced VMs
*   **Managed Instance Groups (MIGs)**: Auto-healing, autoscaling.
*   **Load Balancer**: Distributes traffic; removes unhealthy instances.
*   **Multi-Zone**: Deploy MIG across multiple zones for HA.

### Floating IP Addresses
*   **Use**: Assign static IP to active instance; move to standby on failover.
*   **Pattern**: Keepalived or custom scripts to manage IP reassignment.

## Data Availability

### Cloud Spanner Replication with Striim
*   **Striim**: Real-time replication for Cloud Spanner across regions/clouds.

### Google Workspace Backup (AFI AI)
*   **Third-Party**: Afi AI for backing up Google Workspace data to Cloud Storage.

### HA PostgreSQL on Compute Engine
*   **Architecture**: PostgreSQL with streaming replication across zones.
*   **Failover**: Automatic with tools like Patroni or repmgr.

## Business Continuity with CI/CD
*   **Automated Deployments**: Reduce manual errors.
*   **Infrastructure as Code**: Recreate infrastructure quickly in DR.
*   **Testing**: Automated tests validate deployments in DR environment.
