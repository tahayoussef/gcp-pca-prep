# Manage and optimize cloud resources

- **Goals**
    - Focus on **Efficiency** (automation/analytics), **Performance** (scaling), and **Scalability** (adapting to growth).

- **Right-size Resources**
    - Avoid over-provisioning (waste) and under-provisioning (bottlenecks).
    - Use **Cloud Monitoring** and **Recommender** to identify opportunities.
    - Use custom metrics and alerts to trigger right-sizing actions.

- **Use Autoscaling**
    - Dynamically adjust capacity based on detailed workload fluctuations.
    - **Compute Engine**: Managed Instance Groups (MIGs) with autoscaling policies (CPU, etc.).
    - **GKE**:
        - **Cluster Autoscaler**: Adds/removes nodes.
        - **Horizontal Pod Autoscaler (HPA)**: Scales replicas based on metrics.
        - **Vertical Pod Autoscaler (VPA)**: Adjusts resource requests/limits.
        - **Node Auto-Provisioning**: Creates optimized node pools.
    - **Cloud Run**: Built-in serverless autoscaling (scales to zero).

- **Leverage Cost Optimization Strategies**
    - **Committed Use Discounts (CUDs)**: Commitment for a period (1 or 3 years).
    - **Sustained Use Discounts (SUDs)**: Automatic discounts for usage levels (Compute Engine).
    - **Spot VMs**: Excess capacity at lower cost (preemptible).
    - Use **Cost Management** (Budgets and Alerts) to track spending.

- **Track Resource Usage and Costs**
    - Use **Tags** and **Labels** to categorize resources (e.g., by department, project).
    - Analyze patterns with **Cloud Billing** tools.
    - Create custom dashboards to visualize spending trends.

- **Establish Cost Allocation and Budgeting**
    - Implement chargeback/showback mechanisms to allocate costs to teams.
    - Set budgets for teams/projects to ensure accountability.
