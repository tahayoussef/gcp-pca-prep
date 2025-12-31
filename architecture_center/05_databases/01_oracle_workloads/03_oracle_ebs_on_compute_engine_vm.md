# Oracle E-Business Suite on Compute Engine

## Overview
Deploy **Oracle E-Business Suite (EBS)** on **Compute Engine** with various architecture patterns (zonal, regional, multi-regional).

## Architecture Patterns

### 1. Zonal Architecture
*   All components in single zone.
*   Simplest, lowest cost, but no HA.

### 2. Zonal with DMZ
*   DMZ subnet for web tier; database in private subnet.
*   Improved security.

### 3. Regional Architecture
*   App/DB spread across multiple zones in one region.
*   High availability within region.

### 4. Multi-Regional (DR)
*   Primary region + disaster recovery region.
*   Oracle Data Guard for database replication.
*   Active-passive setup.

## Components
*   **Web Tier**: Load balancer + web servers.
*   **Application Tier**: EBS application servers.
*   **Database Tier**: Oracle Database (single instance or RAC).
*   **Shared Storage**: Persistent Disks or Filestore.

## Design Considerations
*   **Reliability**: Use regional or multi-regional for production.
*   **Performance**: Local SSDs for database; optimize network throughput.
*   **Security**: Private VPC, IAM, OS hardening.
*   **Cost**: Choose architecture based on RTO/RPO requirements.
