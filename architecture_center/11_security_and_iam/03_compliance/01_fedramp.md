# FedRAMP Compliance

The Federal Risk and Authorization Management Program (FedRAMP) is a US government-wide program that provides a standardized approach to security assessment and authorization for cloud products.

## Key Concepts
-   **Standard**: Based on NIST SP 800-53.
    -   **Moderate Control Baseline**: 325 controls.
    -   **High Control Baseline**: 421 controls.
-   **Google Status**: Google Cloud has a **FedRAMP High Provisional Authority to Operate (P-ATO)**. This covers Moderate requirements as well.
-   **Services in Scope**: Over 150 services (including GenAI, ML) are covered by the High P-ATO.

## Implementation (Assured Workloads)
To meet FedRAMP High requirements, you MUST use **Assured Workloads**:
-   **Regulatory Boundary**: Creates a secure folder where guardrails are inherited.
-   **Data Residency**: Restricts resource locations to specific US regions.
-   **Resource Restrictions**: Organization policies restrict the use of non-compliant services.
-   **Sovereignty**: Ensures that only US persons have support access (for IL5/Higher tiers if required).

## Customer Responsibilities
-   **Inheritance**: You inherit controls from the Google Cloud platform.
-   **CRM (Customer Responsibility Matrix)**: Maps out which controls are Google's, which are shared, and which are the customer's responsibility.
-   **SSP (System Security Plan)**: Documentation provided by Google (under NDA) to help customers build their own ATO package.
