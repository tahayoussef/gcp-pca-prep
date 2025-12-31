# FSI perspective: Performance optimization

- **Business Alignment**
    - **KPIs**: Map technology metrics to business outcomes (e.g., faster risk calculations -> tighter spreads).
    - **OKRs**: Connect initiatives to Objectives and Key Results like revenue growth or risk mitigation.

- **HPC & Simulation**
    - **Cloud Bursting**: Burst on-premises HPC workloads to the cloud for elasticity.
    - **Modernization**: Use **Dataflow** for graph-based Monte Carlo simulations (up to 16x faster).
    - **Batch Processing**: Use **Google Distributed Cloud** or **Batch** for massive parallel calculations (XVA).

- **Trading Platforms**
    - **Latency vs. Agility**: While HFT needs <1ms latency (often better suited for **Edge** or specialized colocations), 80% of trading apps benefit more from Cloud resilience and agility.
    - **Cloud-Native**: Build new exchanges on the cloud to leverage global reach and elasticity.
