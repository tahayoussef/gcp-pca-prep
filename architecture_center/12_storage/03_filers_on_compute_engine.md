# File Storage on Compute Engine

## Storage Overview
When choosing file storage for Compute Engine, consider trade-offs between manageability, cost, performance, and scalability.

## Durable Disks (Single VM Access)

### When to Use
- Data accessed by single VM only
- Data doesn't change over time
- Alternative to file server for simpler architectures

### Persistent Disk
- **Format**: Ext4 or XFS file systems
- **Modes**: Read-write or read-only attachment
- **Read-only strategy**: Load data once, attach to hundreds of VMs simultaneously
- **Performance**: Consistent and durable
- **Scaling**: Resizable, no I/O costs after provisioning
- **Types**:
  - Standard: Low-cost, capacity-focused
  - SSD: Best performance with durability

### Hyperdisk
- Advanced persistent disk option
- Dynamic performance optimization
- Higher performance capabilities

### Local SSD
- **Capacity**: Up to 9 TB per instance
- **Performance**: Sub-millisecond latency, millions of IOPS, GB/s bandwidth
- **Benefits**: Doesn't use network bandwidth
- **Trade-offs**: Limited availability, durability, and flexibility
- **Use case**: Ephemeral data requiring extreme performance

## Managed File Storage Solutions

### Filestore Basic
- **Capacity**: Configurable
- **Performance**: Consistent
- **Scaling**: Scale up only
- **Use case**: Standard file sharing needs

### Filestore Zonal
- **Capacity**: Configurable
- **Performance**: Dynamic scaling with custom performance tiers
- **Scaling**: Scale up and down
- **Availability**: Zonal
- **Features**: Snapshots for backup

### Filestore Regional
- **Capacity**: Configurable
- **Performance**: Dynamic scaling with custom performance tiers
- **Availability**: Regional (cross-zone resilience)
- **Features**: Snapshots, improved durability

### Managed Lustre
- **Use case**: High-performance parallel file systems
- **Ideal for**: HPC workloads, AI/ML training
- **Performance**: Very high throughput and IOPS
- **Access pattern**: Parallel access from multiple clients

### NetApp Volumes
- **Features**: Enterprise-grade file storage
- **Capabilities**: Cross-region replication, snapshots, backups
- **Protocols**: Multiple file protocols supported
- **Tiers**: Regional (Flex) or zonal deployments

## Partner Solutions (Cloud Marketplace)

### NetApp Cloud Volumes ONTAP
- Enterprise data management features
- Multi-protocol support
- Advanced data protection

### DDN Infinia
- High-performance parallel file system
- Optimized for HPC and AI/ML workloads

### Nasuni Cloud File Storage
- Global file system
- Cloud-native architecture

### Sycomp Intelligent Data Storage Platform
- Intelligent data management
- Performance optimization

## Key Selection Criteria

### Decision Factors
1. **Management**:
   - Managed services (easiest, SLA provided)
   - Supported solutions (flexible, partner support)
   - Self-managed (most effort, full control)

2. **Durability & Availability**:
   - Most solutions are zonal by default
   - Consider DR requirements for zone/region failures
   - Plan for high availability based on application needs

3. **Access Locations**:
   - Zones and regions where data access is needed
   - Hybrid (on-premises + cloud) access requirements
   - Influence choice of file storage solution

4. **Performance Requirements**:
   - Network bandwidth needs
   - IOPS and latency requirements
   - Machine type and disk capacity considerations

## Best Practices
- Choose correct disk capacity and vCPUs for required bandwidth and IOPS
- Consider network bandwidth limits of VM machine types
- For extreme performance: Local SSD
- For durability and flexibility: Persistent Disk or Hyperdisk
- For shared file access: Managed file storage solutions
- For HPC/AI workloads: Managed Lustre or partner parallel file systems
