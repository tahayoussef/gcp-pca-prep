# Promote modular design

- **Principle Overview**
    - **Modularity**: Decompose systems into independent components with clear interfaces. Enables targeted scaling of specific bottlenecks.

- **Recommendations**
    - **Loose Coupling**: Components should operate independently. If one fails or slows, others continue.
    - **Concurrency**: Design for parallel tasks. Break large jobs into small chunks that can be processed by auto-scaled worker pools.
    - **Stateless Models**: Store state externally (DB/Cache). Allows instances to be added/removed freely without data loss.
    - **Standard Interfaces**: Use APIs and Message Queues (Pub/Sub) to decouple interactions.
