# Website Hosting on Google Cloud

## Overview
Options for hosting websites on Google Cloud, from static sites to complex dynamic applications.

## Hosting Options

### Static Websites
*   **Cloud Storage**: Host static HTML/CSS/JS via bucket with public access.
*   **Firebase Hosting**: CDN-backed static hosting with SSL.

### Dynamic Websites

#### Compute Engine (VMs)
*   Full control, install any software.
*   Use Google Cloud Marketplace for pre-configured stacks (LAMP, WordPress, etc.).
*   **Load Balancing**: Cloud Load Balancing for distribution.
*   **Autoscaling**: Managed Instance Groups.

#### GKE (Containers)
*   Run containerized web apps on Kubernetes.
*   **Ingress**: Expose services via load balancer.
*   **Autoscaling**: Horizontal Pod Autoscaler.

#### Cloud Run (Serverless Containers)
*   Fully managed, scales to zero.
*   Best for stateless HTTP services.

#### App Engine (Platform as a Service)
*   Fully managed platform.
*   Supports multiple languages (Python, Java, Go, PHP, etc.).
*   Automatic scaling, load balancing.

## Common Components
*   **Cloud SQL/Firestore**: Database.
*   **Cloud CDN**: Content delivery for fast global access.
*   **Cloud Armor**: DDoS protection.
*   **Cloud Logging/Monitoring**: Observability.
