# Multi-Cloud Database Management

## Overview
Architectures, use cases, and best practices for managing databases across multiple cloud providers.

## Key Use Cases

### 1. Application Migration
*   Gradual migration from one cloud to another.
*   Database replication for phased cutover.

### 2. Disaster Recovery
*   Database replicas in different clouds for resilience.
*   Asynchronous replication to secondary cloud.

### 3. Cloud Bursting
*   Primary database in one cloud; burst to another during peak load.

### 4. Best-in-Class Services
*   Use best database service from each cloud (e.g., Google BigQuery for analytics, AWS RDS for compatibility).

### 5. Distributed Services
*   Multi-cloud applications with databases distributed geographically.

### 6. Vendor Independence
*   Avoid lock-in by deploying on multiple clouds.

## Deployment Patterns

### 1. Partitioned (No Cross-DB Dependency)
*   Separate databases per cloud; no cross-cloud queries.
*   Simplest pattern.

### 2. Asynchronous Unidirectional Replication
*   Primary in cloud A → replica in cloud B.
*   For DR or read replicas.

### 3. Bidirectional Replication with Conflict Resolution
*   Active-active across clouds.
*   Requires conflict resolution mechanism.

### 4. Fully Active-Active Synchronized
*   Real-time sync across clouds (complex, high cost).

## Database System Categorization
*   **Managed vs Self-Managed**: Cloud native (Cloud SQL, RDS) vs self-deployed (Oracle, MySQL on VMs).
*   **Distributed vs Centralized**: Spanner (globally distributed) vs traditional SQL (single region).

## Best Practices
*   **Existing Systems**: If already using a DB, continue with same vendor across clouds for consistency.
*   **Kubernetes for Portability**: Deploy DB on Kubernetes for easier multi-cloud management.
*   **Built-in Replication vs External**: Use database's native replication when possible; external tools (Striim, Datastream) for heterogeneous replication.
*   **Network Performance**: Ensure low latency between clouds (dedicated interconnects).
