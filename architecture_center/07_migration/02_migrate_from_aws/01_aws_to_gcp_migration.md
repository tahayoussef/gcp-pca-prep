# Migrate from AWS to Google Cloud

## Service Mapping & Migration Paths

### Compute
**EC2 → Compute Engine**: Migrate for Compute Engine; lift-and-shift VMs. Similar instance types available.

**Lambda → Cloud Run**: Containerize Lambda functions; deploy to Cloud Run (serverless containers).

### Storage
**S3 → Cloud Storage**: Storage Transfer Service for automated migration. Similar bucket/object model.

### Containers
**EKS → GKE**: 
- Export Kubernetes manifests from EKS.
- Re-deploy to GKE with minimal changes.
- Use Anthos Config Management for consistency.

### Databases
**RDS MySQL → Cloud SQL MySQL**: Database Migration Service (DMS) for live migration with minimal downtime.

**RDS Aurora (PostgreSQL) → Cloud SQL PostgreSQL**: DMS; Aurora's PostgreSQL compatibility simplifies migration.

**RDS SQL Server → Cloud SQL SQL Server**: DMS; schema and data migration.

## Migration Strategy
1. **Assess**: Inventory AWS resources.
2. **Plan**: Map AWS services to Google Cloud equivalents.
3. **Network**: Set up VPN/Interconnect between AWS and Google Cloud.
4. **Pilot**: Migrate non-critical workloads first.
5. **Data Migration**: Use DMS for databases, Storage Transfer Service for S3.
6. **Cutover**: Switch DNS/traffic to Google Cloud.
7. **Decommission**: Shut down AWS resources after validation.

## Key Considerations
*   **IAM Differences**: AWS IAM roles vs Google Cloud service accounts.
*   **Networking**: VPC peering, Cloud Interconnect for hybrid period.
*   **Cost**: Compare pricing models; optimize Google Cloud usage.
