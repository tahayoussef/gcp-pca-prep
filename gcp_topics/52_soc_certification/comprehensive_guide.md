# SOC Certification - Comprehensive Guide

## Overview
**SOC (System and Organization Controls)** reports are independent third-party audits that verify Google Cloud's compliance with security, availability, and privacy standards.

## Report Types & Differences

| Report | Audience | Focus | Detail Level | Access |
| :--- | :--- | :--- | :--- | :--- |
| **SOC 1** | **Auditors** (Financial) | Internal Controls over **Financial Reporting** (ICFR). | Detailed | **Compliance Reports Manager** (NDA/Login req). |
| **SOC 2** | **Customers/Partners** | **Security**, Availability, Confidentiality (Trust Services Criteria). | Detailed (Technical controls) | **Compliance Reports Manager** (NDA/Login req). |
| **SOC 3** | **Public** | Same as SOC 2 (Security/Availability). | Summary (High-level) | **Public** (Compliance Reports Manager). |

## Exam Focus Areas

1.  **Financial Application**:
    - "Customer is migrating a payroll or banking application and their auditor needs assurance." -> **SOC 1**.

2.  **SaaS Provider**:
    - "You are building a SaaS on GCP and your customers want to know if GCP is secure." -> Provide **SOC 2** (if NDA) or **SOC 3** (public).

3.  **Type I vs Type II**:
    - **Type I**: Point in time (Design of controls).
    - **Type II**: Period of time (Design + **Operating Effectiveness**). Type II is "better" for long-term assurance.
