# AI and ML perspective: Performance optimization

- **Define Objectives**
    - **Trade-offs**: Balance Accuracy vs Latency vs Cost based on business needs (e.g., Real-time fraud detection needs low latency; Offline batch analysis needs high accuracy).

- **Experimentation**
    - **Environment**: Establish a dedicated environment for rapid experimentation, separate from Prod.
    - **Tracking**: Track experiments (hyperparameters, metrics, code versions) to ensure reproducibility.

- **Training & Serving**
    - **Hardware**: Choose appropriate accelerators (**TPUs** for large matrix math, **GPUs** for general deep learning) for the workload.
    - **Pre-trained Models**: Use Foundation Models (**Vertex AI Model Garden**) instead of training from scratch where possible to save time/compute.
    - **Optimization**: Optimize data pipelines (I/O bound vs Compute bound) to ensure accelerators are fed data fast enough.
