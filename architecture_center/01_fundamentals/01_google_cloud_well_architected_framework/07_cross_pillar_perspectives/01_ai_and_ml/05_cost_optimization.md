# AI and ML perspective: Cost optimization

- **Measure Costs & Returns**
    - **KPIs**: Define Business Value (ROI) and Unit Costs (Cost per Prediction).
    - **Visibility**: Use **Cloud Billing** and **Looker** dashboards to visualize AI spend.

- **Efficient Resources**
    - **Autoscaling**: Configure autoscaling to scale down (even to zero for **Cloud Run** or **Vertex Endpoints**) when idle.
    - **Spot VMs**: Use Preemptible/Spot VMs for training jobs that can be checkpointed and resumed.
    - **Rightsizing**: Don't use a massive GPU if a smaller one (or CPU) suffices for inference.

- **Development Efficiency**
    - **Notebooks**: Use managed **Vertex AI Workbench** or **Colab Enterprise** for collaborative, on-demand development environments.
    - **Reusability**: Use **Vertex AI Feature Store** to share features across teams and avoid re-computing them.
