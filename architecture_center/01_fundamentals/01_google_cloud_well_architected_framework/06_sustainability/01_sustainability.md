# Design for environmental sustainability

- **Principle Overview**
    - **Goal**: Minimize the environmental impact (carbon footprint) of cloud workloads.

- **Understand Your Footprint**
    - **Tools**: Use the **Carbon Footprint Dashboard** to track emissions by project and service.

- **Choose Regions and Services**
    - **Regions**: Select regions with lower carbon intensity ("Low CO2" or "water-free" regions). Use **Google Cloud Region Picker**.
    - **Services**: Prefer **Serverless** and managed services over self-managed VMs (higher utilization efficiency).
    - **Compute**: Migrate on-prem VMs to **Compute Engine** (generally more efficient than on-prem datacenters).

- **Minimize Idle Resources**
    - **Idle VMs**: Identify and delete/stop unused instances using **Active Assist** recommendations.
    - **Rightsizing**: Avoid over-provisioning machine types.
    - **Architecture**: Move away from simple "Lift-and-Shift" to optimized cloud-native designs.

- **Batch Workloads**
    - **Scheduling**: Run batch jobs during times of lower grid carbon intensity or in cleaner regions.
