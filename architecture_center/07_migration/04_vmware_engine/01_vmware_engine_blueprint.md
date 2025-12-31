# VMware Engine Blueprint

## Overview
**Google Cloud VMware Engine**: Fully managed VMware infrastructure (vSphere, vSAN, NSX-T) running on Google Cloud.

## Use Cases
*   **Lift-and-Shift**: Migrate VMware VMs to Google Cloud without conversion.
*   **Disaster Recovery**: DR for on-prem VMware to Google Cloud.
*   **Hybrid Cloud**: Extend on-prem VMware to Google Cloud.

## Architecture
*   **Private Cloud**: Dedicated VMware SDDC (software-defined data center) in Google Cloud.
*   **Networking**: Connect via Cloud Interconnect or VPN.
*   **Integration**: Access Google Cloud services (BigQuery, Cloud SQL, etc.) from VMware VMs.

## Migration
*   **HCX (Hybrid Cloud Extension)**: VMware tool for migrating VMs with minimal downtime.
*   **vMotion**: Live migrate VMs from on-prem to VMware Engine.

## Benefits
*   Native VMware experience; no re-architecture needed.
*   Managed service; Google handles infrastructure.
*   Access to Google Cloud services.
