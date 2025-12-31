# Design for graceful degradation

- **Principle Overview**
    - **Graceful Degradation**: Maintain system availability (possibly with reduced functionality) during high load or partial failure, rather than crashing completely.
    - **Example**: Serving cached/older results instead of failing a search query.

- **Recommendations**
    - **Throttling**: Rate-limit incoming requests (e.g., with **Apigee**) to protect backend services from being overwhelmed.
    - **Load Shedding**: Drop excess requests at the Load Balancer/Frontend level ("fail fast") to preserve capacity for handled requests.
    - **Retry Logic**: Implement exponential backoff and jitter for retries to avoid "thundering herd" problems.
    - **Test Overload**: Simulate traffic spikes to validate throttling mechanisms.
