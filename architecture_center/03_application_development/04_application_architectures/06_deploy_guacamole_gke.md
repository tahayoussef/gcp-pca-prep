# Apache Guacamole on GKE and Cloud SQL

## Overview
Deploy **Apache Guacamole** (clientless remote desktop gateway) on **GKE** with **Cloud SQL** backend.

## Architecture
*   **Guacamole Frontend**: Deployed on GKE (web interface).
*   **Guacamole Backend (`guacd`)**: Deployed on GKE (proxy server).
*   **Database**: Cloud SQL (MySQL/PostgreSQL) for configuration storage.
*   **Load Balancer**: Cloud Load Balancing for HA.

## Use Case
*   Remote desktop access to VMs via web browser (no client software needed).
*   Supports RDP, VNC, SSH protocols.
