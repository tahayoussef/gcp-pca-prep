# Define reliability based on user-experience goals

- **Principle Overview**
    - Reliability should be measured by its impact on users, not just internal system metrics (like CPU usage).
    - Differentiate between internal issues and user-facing outages.

- **Measure User Experience**
    - **Metrics**: Focus on success ratios, application latency, and error rates from the user's perspective.
    - **Collection Point**: Ideally collect data from the client (device/browser). If not, use the Load Balancer or Frontend as the proxy.

- **Analyze User Journeys**
    - **Tracing**: Use **Cloud Trace** to track a request's path through microservices.
    - **Goal**: Identify bottlenecks and latency sources across the entire architecture.
