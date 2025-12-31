# Single-zone deployment on Compute Engine

- **Architecture**
    - **IaaS Model**: Uses Compute Engine VMs in a single zone.
    - **Network**: Regional External LB -> Web Tier (MIG) -> Regional Internal LB -> App Tier (MIG) -> Database (VM).
    - **Storage**: Zonal Persistent Disks.
    - **Resilience**: Vulnerable to zone outage.

- **Design Patterns**
    - **Failover**: Maintain a passive replica in a different zone (failover zone).
    - **Backups**: Store backups in **Regional Cloud Storage** buckets to survive zone failure.
    - **Autohealing**: Use MIG autohealing to recover from VM crashes.

- **Reliability**
    - **Availability**: 99.9% target.
    - **Outage**: During zone outage, application is down unless manual/automated failover to standby zone is invoked.
