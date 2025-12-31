# Optimize resource usage

- **Choose Resources based on Requirements**
    - **Environment-specific**: Match resource class (HA vs. cost-efficient) to the environment (Prod vs. Dev).
    - **Workload-specific**: Select services aligned with workload needs (e.g., **Spanner** for global consistency, **Spot VMs** for batch jobs).

- **Select Regions Strategically**
    - Evaluate regions based on **cost**, latency, and sustainability requirements.

- **Use Built-in Optimization Options**
    - **Compute**: Autoscaling, Custom Machine Types, Spot VMs, Schedule VMs (stop/start).
    - **GKE**: Cluster Autoscaler, Node Auto-Provisioning.
    - **Storage**: Object Lifecycle Management, Autoclass (dynamic class transition).
    - **BigQuery**: Capacity-based pricing, Partitioning/Clustering.

- **Optimize Resource Sharing**
    - Share infrastructure where secure (e.g., multi-tenant GKE clusters, shared Cloud SQL for non-prod).
    - Use **GKE Autopilot** for bin-packing efficiency.

- **Develop Reference Architectures**
    - Maintain specific **Blueprints** with pre-approved, cost-optimized configurations.
    - Speeds up deployment and ensures consistency.

- **Enforce Cost Discipline**
    - Use **Organization Policies** to restrict expensive resource locations or products.
    - Set granular **Quotas** (project, service, resource) to prevent cost overruns.
    - Establish **Budgets** and configure proactive alerts.
