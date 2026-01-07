# PCI DSS Compliance

Payment Card Industry Data Security Standard (PCI DSS) compliance is required for any entity that processes, stores, or transmits credit card data.

## Strategies for Scope Reduction
The primary goal is to minimize the **Cardholder Data Environment (CDE)** scope.
1.  **Resource Hierarchy**: Use dedicated folders and projects to isolate CDE resources from the rest of the organization.
2.  **Network Segmentation**: 
    -   Use **Shared VPC** to centralize network control.
    -   Isolate subnets containing CDE workloads.
    -   Use firewall rules to strictly control ingress/egress to the CDE.
3.  **VPC Service Controls**: Create a service perimeter around projects in the CDE to prevent data exfiltration.
4.  **Tokenization**: Replace sensitive PAN (Primary Account Numbers) with tokens.
    -   **Tokenizer Service**: Use Cloud Run functions and Cloud KMS to encrypt/decrypt card data.
    -   Only the tokenizer service should touch the actual card data.

## PCI on GKE Blueprint
-   **Project Layout**:
    -   `Network Host`: Shared VPC.
    -   `Management`: Logging/Monitoring.
    -   `In-scope`: GKE cluster for card processing.
    -   `Out-of-scope`: GKE cluster for other services.
-   **Security Controls**: 
    -   **mTLS**: Use a service mesh (Istio/Cloud Service Mesh) for encrypted pod-to-pod communication.
    -   **Binary Authorization**: Ensure only signed images are deployed.
    -   **Shielded GKE Nodes**: For environment integrity.
