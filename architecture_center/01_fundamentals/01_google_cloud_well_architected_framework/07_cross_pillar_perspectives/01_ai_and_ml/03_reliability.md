# AI and ML perspective: Reliability

- **Scalability**
    - **Training**: Use **Vertex AI Custom Training** or **Dataflow** with horizontal autoscaling. Use **Spot VMs** for fault-tolerant batch training to reduce costs.
    - **Inference**: Use **Vertex AI Endpoints** with autoscaling (min/max replicas) or **GKE** with **Horizontal Pod Autoscaling (HPA)** based on GPU/TPU metrics.

- **Modular Architecture**
    - **Decoupling**: Separate Training and Serving. Use standard APIs (REST/gRPC) to interface between components.
    - **Microservices**: Break down complex pipelines into small, reusable steps.

- **MLOps & Quality**
    - **Automation**: Automate deployment to reduce manual errors.
    - **Validation**: Validate input data quality (schema checks, nulls) and output model quality (accuracy thresholds) automatically.

- **Observability**
    - **Infrastructure Monitoring**: Track CPU, Memory, GPU utilization to ensure resources are available.
    - **Reliability Metrics**: Track error rates, latency, and throughput of inference endpoints.
