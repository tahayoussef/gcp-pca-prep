# Foster a culture of cost awareness

- **Provide Organization-Wide Cost Visibility**
    - Standardize cost calculation and budgeting.
    - Use visibility tools (e.g., **Google Cloud Billing dashboard**) for real-time insights.
    - Implement **Cost Allocation** and chargeback to assign costs to teams/projects.
    - Promote transparency and discuss cost implications early.

- **Understand Billing Models**
    - Be aware of pricing differences across regions and resource types (fixed vs. usage-based).
    - Use the **Pricing Calculator**.

- **Understand Cost Optimization Options**
    - **Resource-based**: Right-sizing, autoscaling, always-allocated CPUs (Cloud Run), BigQuery slot commitments.
    - **Discount-based**:
        - **Committed Use Discounts (CUDs)**: predictable usage.
        - **Sustained Use Discounts (SUDs)**: automatic for continuous usage.
        - **Spot VMs**: fault-tolerant workloads (cheaper, preemptible).

- **Incorporate Cost Estimates**
    - Include estimates in architecture blueprints to compare options proactively.

- **Use Consistent Labels**
    - Define a formal **Labeling Policy** to track costs by project, department, or cost center.
    - Automate labeling with tools like Terraform.

- **Share Cost Reports**
    - Empower teams with periodic reports, automated notifications (anomalies/budget alerts), and dashboards.
    - Use **FinOps Hub** for recommendations.
    - Create custom dashboards with **BigQuery** and **Looker Studio** for granular analysis.
