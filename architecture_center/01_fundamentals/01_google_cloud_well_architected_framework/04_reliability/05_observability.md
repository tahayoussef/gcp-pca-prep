# Detect potential failures by using observability

- **Principle Overview**
    - **Observability**: Using Metrics (SLIs), Logs (Events), and Traces (Journeys) to understand system behavior.
    - **Goal**: Detect failures before they impact users.

- **Gain Comprehensive Insights**
    - **Tools**: **Cloud Monitoring** (metrics) and **Cloud Logging** (logs).
    - **Custom Metrics**: Create custom metrics via SDK for business-specific logic.

- **Proactive Troubleshooting**
    - **Logging**: Enable access logs (Cloud Storage) and network logs (**VPC Flow Logs**) for deep visibility.
    - **Cost Control**: Use **Exclusion Filters** in Cloud Logging to discard low-value logs and manage costs.

- **Alerting**
    - **Strategy**: Alert on symptoms that affect user experience (SLO violations) rather than just transient system causes.
    - **Management**: Set thresholds to avoid alert fatigue.
