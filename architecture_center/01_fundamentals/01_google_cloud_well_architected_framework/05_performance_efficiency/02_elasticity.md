# Take advantage of elasticity

- **Principle Overview**
    - **Elasticity**: Capabilities to scale resources up (Vertical) or out (Horizontal) dynamically based on load.

- **Plan for Peak Load**
    - **Scheduled Scaling**: Manually pre-scale for *known* events (e.g., seasonal sales).
    - **Autoscaling**: Use automated policies (CPU utilization, Queue depth) for *unexpected* surges.

- **Use Predictive Scaling**
    - **Forecasting**: **Compute Engine** Predictive Autoscaling uses historical data to scale out *before* load arrives, reducing latency spikes.

- **Serverless & Managed**
    - **Serverless**: Use **Cloud Run**, **Cloud Functions**, **BigQuery**, **Spanner** for "scale to zero" and instant elasticity without managing infra.
    - **Kubernetes**: Use **GKE Autopilot** for fully managed node/pod scaling.
