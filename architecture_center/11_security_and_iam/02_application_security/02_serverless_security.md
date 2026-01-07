# Secured Serverless Architecture

Securing serverless workloads (Cloud Run, Cloud Functions) involves securing identity, network, and configuration.

## Identity and Access
-   **Service Identity**: Every serverless service runs as a **Service Account**. Adhere to **Least Privilege** by giving this account only necessary permissions.
-   **Invocation Access**: Control who can invoke the service (public unauthenticated vs. private authenticated) using IAM roles (`Cloud Run Invoker`, `Cloud Functions Invoker`).

## Network Security
-   **Ingress Controls**:
    -   **Internal Only**: Restrict traffic to within the VPC or specific load balancers.
    -   **VPC Service Controls**: Place services inside a service perimeter to prevent data exfiltration.
-   **Egress Controls**:
    -   **Serverless VPC Access**: Use a connector (or Direct VPC Egress in Cloud Run) to allow the service to access internal VPC resources (like private requested DBs) without traversing the public internet.

## Configuration Security
-   **Secrets Management**: Store API keys and passwords in **Secret Manager** and mount them as environment variables or volumes. Do NOT hardcode secrets.
-   **Container Security**:
    -   Use minimal base images (distroless).
    -   Scan images for vulnerabilities (Artifact Analysis).
    -   **Binary Authorization**: Ensure only trusted/signed images can be deployed.

## Isolation
-   **Cloud Run Gen 2**: Provides gVisor-based sandbox isolation for strong multi-tenant security.
