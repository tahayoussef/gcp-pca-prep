# Decide a Resource Hierarchy

## Overview
The Google Cloud resource hierarchy (Organization > Folders > Projects) structures your resources to map to your organization's operational model. It dictates how policies are inherited and how billing is aggregated.

## Design Factors
*   **Responsibility**: Who manages the resources (departments, subsidiaries)?
*   **Compliance**: Do certain environments need strict isolation?
*   **Business Structure**: Account for mergers, acquisitions, and spin-offs.

## Architecture Options

### Option 1: Based on Application Environments
Structure the hierarchy around lifecycle stages (e.g., Development, Testing, Production).
*   **Pros**: 
    *   Standardized policies per environment (e.g., stricter security in Production).
    *   Clear separation of duties (QA teams vs. Audit teams).
*   **Use Case**: Unified definition of "Production" across the company, centralized security enforcement.
*   **Diagram Concept**: `Org -> [Prod | Non-Prod] -> [App1 | App2]`

### Option 2: Based on Regions or Subsidiaries
Structure the hierarchy around business units or geographies.
*   **Pros**:
    *   autonomy for distinct business units or regions.
    *   Supports different operational models or regulatory requirements per region.
*   **Use Case**: Global conglomerates, acquired subsidiaries with independent IT, or strict data residency rules.
*   **Diagram Concept**: `Org -> [Subsidiary A | Subsidiary B] -> [Region X | Region Y]`

## Managing Interactions
*   **Policy Inheritance**: Organization Policies and IAM allow policies descend; deny policies can restrict specific actions at higher levels.
*   **Logging**: Use Aggregated Sinks to centralize logs from all projects at the Folder or Organization level.
*   **Billing**: Costs are associated with Projects but can be reported on and analyzed by Folder hierarchy.
