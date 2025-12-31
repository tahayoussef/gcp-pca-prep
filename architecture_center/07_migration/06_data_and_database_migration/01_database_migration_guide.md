# Database Migration Concepts and Principles

## Part 1: Planning and Assessment

### Migration Strategies
*   **Homogeneous**: Same database type (e.g., MySQL → Cloud SQL MySQL). Simpler.
*   **Heterogeneous**: Different database type (e.g., Oracle → PostgreSQL). Requires schema conversion.

### Assessment
*   **Compatibility Analysis**: Check if source DB features are supported in target.
*   **Schema Complexity**: Stored procedures, triggers, custom functions may need rewriting.
*   **Data Volume**: Estimate migration time based on data size and bandwidth.

### Migration Approaches
*   **Offline Migration**: Shutdown source DB, migrate data, cutover. Downtime = migration time.
*   **Online Migration (CDC)**: Continuous replication; minimal downtime. Use Database Migration Service.

## Part 2: Migration Execution and Validation

### Database Migration Service (DMS)
*   Supports MySQL, PostgreSQL, SQL Server, Oracle.
*   **Continuous Replication**: Keeps target in sync during migration.
*   **Minimal Downtime**: Cutover when ready.

### Migration Steps
1. **Prepare Source**: Enable binary logging (MySQL), WAL (PostgreSQL).
2. **Create Target**: Provision Cloud SQL/AlloyDB instance.
3. **Configure DMS**: Set up migration job (source, target, connectivity).
4. **Initial Load**: Full data copy.
5. **CDC**: Continuous replication of changes.
6. **Validation**: Compare data, test queries.
7. **Cutover**: Switch applications to target; stop replication.

### Validation
*   **Row Counts**: Ensure all rows migrated.
*   **Checksums**: Verify data integrity.
*   **Application Testing**: Test all queries, transactions.
*   **Performance Testing**: Ensure target meets performance requirements.

### Post-Migration
*   Monitor target database.
*   Optimize queries for target platform.
*   Decommission source after validation period.
