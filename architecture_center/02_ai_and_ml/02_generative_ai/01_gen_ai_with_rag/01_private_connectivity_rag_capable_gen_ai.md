# Private Connectivity for RAG-Capable Generative AI Applications

## Overview
Implements **network infrastructure** to improve security for RAG applications using **private connectivity** (no public internet).

## Architecture
*   **External Network**: Data engineers upload data via **Cloud Interconnect** or **HA VPN**.
*   **Routing VPC Network**: 
    *   Terminates external connectivity.
    *   Hosts **Network Connectivity Center Hub** to connect all networks.
    *   Contains **Private Service Connect endpoint** for Cloud Storage.
*   **RAG VPC Network** (Shared VPC):
    *   **Data Ingestion Subsystem**: Cloud Storage (raw data) → Processing → RAG Datastore.
    *   **Serving Subsystem**: RAG Datastore → Serving Processes → Model → Response.
    *   **Frontend Subsystem**: Regional Internal Application Load Balancer → Cloud Run/GKE → Users.

## Traffic Flows
1.  **RAG Population**: External Network → Private Service Connect → Cloud Storage → Data Ingestion → Vector Store.
2.  **Inference**: External Network → Load Balancer → Serving Subsystem → Model → Response.

## Key Features
*   **Network Connectivity Center**: Links external, routing, and RAG VPC networks.
*   **Private Google Access**: Workloads without external IPs access Google APIs over private infrastructure.
*   **VPC Service Controls**: Enforce security perimeters.
