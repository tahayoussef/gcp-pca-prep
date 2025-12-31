# Automate Utilization Review of Health Insurance Claims

## Overview
Reference architecture for automating **Prior Authorization (PA)** processing and **Utilization Review (UR)** for health insurance using Gen AI.

## Architecture

### Claims Data Activator (CDA)
*   Extracts data from unstructured sources (forms, documents).
*   Ingests into database in structured, machine-readable format.
*   Uses **Document AI** for form parsing.

### Utilization Review Service (UR Service)
*   Integrates PA request data + policy documents + care guidelines.
*   Generates **approval/denial recommendations** using **Vertex AI Generative AI**.
*   Human-in-the-loop for final review.

## Key Features
*   **Automated PA Processing**: Reduces manual review time.
*   **AI-Driven Recommendations**: Grounds decisions in policy and medical guidelines.
*   **Compliance**: Designed for healthcare regulations.
