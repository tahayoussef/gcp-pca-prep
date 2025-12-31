# Global deployment with Compute Engine and Spanner

- **Architecture**
    - **Global Distribution**: Resources distributed globally.
    - **Network**: **Global External Application LB** -> Regional MIGs -> **Cross-region Internal LB** -> App Tier.
    - **Database**: **Cloud Spanner** (Multi-region active-active).
    - **Storage**: Application servers use regional PDs, but data state is in Spanner.

- **Design Patterns**
    - **Spanner**: 4 Read-Write replicas across 2 regions + 1 Witness (minimum for multi-region). Synchronous replication.
    - **Cross-Region LB**: Internal traffic can flow across regions if needed (though typically kept local for latency).

- **Reliability**
    - **Consistency**: Strong consistency globally via Spanner.
    - **Survivability**: Can survive region failure with zero data loss (RPO=0) and automatic failover (RTO~0).
