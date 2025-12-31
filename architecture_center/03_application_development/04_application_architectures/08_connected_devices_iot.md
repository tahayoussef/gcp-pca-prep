# Connected Devices (IoT) Architecture

## Overview
Reference architectures for Internet of Things (IoT) deployments on Google Cloud.

## Key Patterns

### 1. MQTT Broker Architecture
*   **Devices** → **MQTT Broker** (e.g., Eclipse Mosquitto on GKE) → **Pub/Sub** → Processing.
*   For devices that require MQTT protocol.

### 2. IoT Platform Architecture
*   **Devices** → **Cloud IoT Core** (deprecated; use partner solutions) → **Pub/Sub** → Processing.
*   Managed device registry and authentication.

### 3. Device-to-Pub/Sub Direct
*   **Devices** → **Pub/Sub** directly (if devices support HTTP/gRPC).
*   Simplest architecture.

## Processing & Storage
*   **Pub/Sub** → **Dataflow** (stream processing) → **BigQuery/Bigtable** (storage).
* AI/ML for anomaly detection, predictive maintenance.

## Security Best Practices
*   Device authentication (certificates, tokens).
*   Private connectivity (VPN, Cloud Interconnect).
*   Data encryption in transit and at rest.

## Device Provisioning
*   Secure provisioning processes for bare-metal devices.
*   Certificate-based authentication.
