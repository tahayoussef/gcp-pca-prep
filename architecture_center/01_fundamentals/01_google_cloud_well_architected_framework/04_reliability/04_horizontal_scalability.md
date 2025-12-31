# Take advantage of horizontal scalability

- **Principle Overview**
    - **Horizontal Scaling (Scale Out)**: Adding more machine instances. Preferred over Vertical Scaling (Scale Up) which has hardware limits and cost spikes.
    - **Resilience**: Horizontal scaling reduces the impact of a single node failure.

- **Use Managed Services**
    - **Compute Engine**: Use **Managed Instance Groups (MIGs)** to auto-scale VMs based on load (CPU, queries).
    - **Serverless**: Use **Cloud Run** or **Cloud Functions** which scale to zero and up automatically.

- **Design for Scaling**
    - **Modular Design**: Break applications into smaller, independent components that can scale individually.
    - **Statelessness**: Store application state (sessions, data) in external services (Cloud SQL, Redis, Firestore) so instances can be added/removed without data loss.
