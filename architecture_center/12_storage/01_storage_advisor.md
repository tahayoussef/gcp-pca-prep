# Design an Optimal Storage Strategy

## Overview
- Three-phase design process for cloud storage:
  1. **Define requirements**: Assess workload characteristics, security, resilience, performance, and cost
  2. **Review options**: Evaluate available GCP storage services
  3. **Choose storage**: Select services based on requirements

## GCP Storage Options

### Block Storage
- **Persistent Disk**
  - Capacity: 10 GiB to 64 TiB per disk, up to 257 TiB per VM
  - Features: Zonal or regional replication, snapshots, disk cloning
  - Performance: Linear scaling with consistent performance
  - Encryption: Google-managed, customer-managed, or customer-supplied keys
  
- **Hyperdisk**
  - Capacity: 4 GiB to 64 TiB per disk, up to 512 TiB per VM
  - Features: Dynamic scaling, optimized performance
  - Encryption: Google-managed, customer-managed, or customer-supplied keys

- **Local SSD**
  - Capacity: 375 GiB per disk, up to 12 TiB per VM (Titanium SSD available for higher capacity)
  - Use case: Ephemeral data requiring sub-millisecond latency and high IOPS
  - Trade-offs: Limited availability, durability, and flexibility

### File Storage
- **Filestore**
  - **Basic**: 1 TiB to 10 PiB, scale up only
  - **Zonal/Regional**: 1 TiB to 10 PiB, scale up and down
  - Features: NFS protocol, snapshots (Zonal/Regional), backups, replication
  - Performance: Basic has consistent performance; Zonal/Regional support dynamic scaling
  - Encryption: Customer-managed keys available for Zonal/Regional tiers

- **Managed Lustre**
  - Capacity: 10 TiB to 1 PiB per storage pool
  - Use case: High-performance parallel file system for HPC and AI/ML workloads
  - Features: High throughput and IOPS

- **NetApp Volumes**
  - Capacity: 1 GiB to 1 PiB per volume
  - Features: Cross-region replication, snapshots, backups
  - Tiers: Regional (Flex) or zonal

### Object Storage
- **Cloud Storage**
  - Location types: Multi-region, dual-region, single region
  - Storage classes: Standard, Nearline, Coldline, Archive
  - Features: Global access, CDN integration, object versioning
  - Redundancy: Data redundancy across zones, optional cross-region redundancy
  - Access control: Uniform or fine-grained
  - Encryption: Google-managed, customer-managed, or customer-supplied keys

## Key Configuration Decisions

### Persistent Disk & Hyperdisk
- Deployment region/zone and replication strategy
- Disk type, size, IOPS (Extreme), throughput (Hyperdisk)
- Encryption keys
- Snapshot schedule

### Filestore
- Service tier (Basic, Zonal, Regional)
- Capacity and IP range
- Access control policies

### Cloud Storage
- Location type and storage class
- Access control model (uniform vs. fine-grained)
- Retention policies
- Encryption type

## Selection Criteria
- **Single VM access**: Use Persistent Disk or Hyperdisk
- **Shared file access**: Use Filestore, Managed Lustre, or NetApp Volumes
- **Object storage with global access**: Use Cloud Storage
- **High-performance HPC/AI workloads**: Use Managed Lustre or Local SSD
- **Cost-sensitive archival**: Use Cloud Storage Archive class
