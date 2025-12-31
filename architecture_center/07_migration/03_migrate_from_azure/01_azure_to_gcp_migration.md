# Migrate from Azure to Google Cloud

## Service Mapping & Migration Paths

### Compute
**Azure VMs → Compute Engine**: Migrate for Compute Engine; similar VM families (general-purpose, compute-optimized, memory-optimized).

### Containers
**AKS → GKE**: Export Kubernetes configs; re-deploy to GKE.

### Storage
**Azure Blob Storage → Cloud Storage**: Storage Transfer Service; similar blob/object storage model.

### Databases
**Azure SQL Managed Instance → Cloud SQL SQL Server**: Database Migration Service.

**Azure SQL Database → Cloud SQL SQL Server**: DMS with schema conversion.

**Azure Database for MySQL → Cloud SQL MySQL**: DMS; straightforward migration.

**Azure Database for PostgreSQL → Cloud SQL PostgreSQL / AlloyDB**: DMS; AlloyDB offers higher performance for PostgreSQL workloads.

**SQL Server (on Azure VM) → Cloud SQL / AlloyDB PostgreSQL**: Migrate SQL Server to PostgreSQL using schema conversion tools + DMS.

## Migration Strategy
1. **Inventory**: Catalog Azure resources.
2. **Service Mapping**: Identify Google Cloud equivalents.
3. **Connectivity**: Azure ExpressRoute + Cloud Interconnect for hybrid setup.
4. **Data Migration**: DMS for databases, Storage Transfer Service for blobs.
5. **Testing**: Validate in Google Cloud environment.
6. **Cutover**: Switch traffic to Google Cloud.

## Key Considerations
*   **Identity**: Azure AD vs Google Cloud Identity; federate or sync.
*   **Networking**: VNet ↔ VPC connectivity during transition.
*   **Licensing**: SQL Server licensing (BYOL or license-included).
