# Distributed Hybrid/Multicloud Pattern
Workloads distributed across on-prem and cloud(s) with interdependencies. **Use**: Gradual migration; hybrid apps needing both environments.

# Tiered Hybrid Pattern
Different tiers (web, app, DB) in different environments. **Example**: Web tier in cloud, database on-prem. **Use**: Keep sensitive data on-prem.

# Partitioned Multicloud Pattern
Independent workloads on different clouds (no cross-cloud dependencies). **Use**: Separate projects/teams; vendor diversification.

# Analytics Hybrid/Multicloud Pattern
Data collection on-prem/edge; analytics in cloud. **Use**: IoT, retail analytics. Tools: BigQuery, Dataflow.

# Edge Hybrid Pattern
Processing at edge (on-prem/IoT devices); cloud for aggregate analytics. **Use**: Low-latency requirements, bandwidth constraints.

# Environment Hybrid Pattern
Different environments (dev, test, prod) across on-prem and cloud. **Use**: Cost savings (dev/test in cloud, prod on-prem or vice versa).

# Business Continuity Patterns
DR and backup across environments. **Patterns**: Active-passive DR, backup to cloud, multi-cloud active-active.

# Cloud Bursting Pattern
Primary workload on-prem; burst to cloud during peak demand. **Use**: Handle traffic spikes cost-effectively.
