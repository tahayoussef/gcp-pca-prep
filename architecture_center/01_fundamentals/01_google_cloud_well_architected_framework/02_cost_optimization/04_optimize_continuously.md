# Optimize continuously

- **Focus on Business-Relevant Metrics**
    - Track **User Experience** (latency, error rates) and **Business Outcomes** (revenue, engagement).
    - Use **DORA metrics** to improve delivery efficiency.
    - Use **SRE metrics** (Error Budgets) to balance innovation and reliability.

- **Use Observability for Optimization**
    - Monitor **Utilization** (CPU, memory) to identify idle resources (e.g., via **Active Assist**).
    - Review cost breakdowns for GKE and other services.
    - Correlate utilization with performance to identify downgrade opportunities without impact.

- **Balance Troubleshooting with Cost**
    - Collect sufficient data but avoid excessive storage costs.
    - Use **Sampling** and **Aggregation**.
    - **Tailor Data Collection**: Define retention policies based on roles (Developers vs. Admins) and regulatory requirements.

- **Implement Smart Alerting**
    - Prioritize alerts that affect customers.
    - Tune thresholds to avoid noise from temporary self-healing issues.
    - Choose appropriate notification channels based on severity.
