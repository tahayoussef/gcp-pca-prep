# Patterns for Scalable and Resilient Apps

## Overview
Patterns and practices for creating applications that are both **scalable** (handle varying workloads) and **resilient** (withstand failures).

## Key Themes
1.  **Automation**: Automate infrastructure provisioning, testing, and deployments to reduce errors and increase consistency.
2.  **Loose Coupling**: Design systems as independent components for flexibility and resilience.
3.  **Data-Driven Design**: Use metrics and logs to make scaling and health decisions.

## Best Practices

### Infrastructure
*   **Infrastructure as Code (IaC)**: Automate provisioning for consistency.
*   **Immutable Infrastructure**: Replace instead of updating to avoid configuration drift.
*   **Physical Distribution**: Distribute resources across regions/zones for fault tolerance.
*   **Managed Services**: Prefer managed services for reduced operational overhead.

### High Availability
*   **Load Balancing**: Balance at each tier (frontend, backend, database).
*   **Multi-Region Deployment**: Deploy across regions for disaster recovery.

### Scaling
*   **Autoscaling**: Configure autoscaling (GKE, Compute Engine) based on metrics.
*   **Minimize Startup Time**: Use pre-baked images, containers, and optimize app startup.
*   **Baseline Resources**: Set baseline, then autoscale up/down based on demand.

### Architecture
*   **Modular/Microservices**: Break app into independent services.
*   **Statelessness**: Design stateless services for easier horizontal scaling.
*   **Service Communication**: Use asynchronous messaging (Pub/Sub) for decoupling.

### Database & Storage
*   **Choose Right DB**: Relational (Cloud SQL/Spanner), NoSQL (Firestore/Bigtable), or object storage (Cloud Storage).
*   **Caching**: Implement caching (Memorystore) to reduce database load.

### Monitoring
*   **Monitor at All Levels**: Infrastructure, app, and user experience.
*   **Health Probes**: Expose readiness and liveness endpoints.
*   **SLOs**: Define Service Level Objectives and track them.

### Development Practices
*   **Testability**: Design for automated testing.
*   **CI/CD**: Automate deployments.
*   **SRE Practices**: Embrace failure as inevitable; design for graceful degradation.

## Testing
*   **Resilience Testing**: Chaos engineering to test failure scenarios.
*   **Load Testing**: Test scaling behavior under realistic loads.
