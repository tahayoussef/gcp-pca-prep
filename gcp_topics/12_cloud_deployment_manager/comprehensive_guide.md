# Cloud Deployment Manager - Comprehensive Guide

## Overview
**Cloud Deployment Manager** is Google Cloud's native **Infrastructure as Code (IaC)** service. It allows you to define resources in declarative configuration files (YAML) and templates (Python/Jinja2).

> [!WARNING]
> Deployment Manager is being deprecated in favor of **Infrastructure Manager** (Terraform). However, legacy questions about "GCP native IaC tool" may still appear on the exam.

## Key Concepts
- **Configuration (YAML)**: The "master" file that lists resources to deploy.
- **Templates (Jinja2/Python)**: Reusable components. (e.g., A template to create a standardized VM with Logging agent installed).
- **Manifest**: Read-only record of the deployment state.
- **Preview Mode**: `gcloud deployment-manager deployments create --preview`. Use this to validate changes without actually creating resources (like `terraform plan`).

## Features
- **Parallel Deployment**: Creates resources in parallel where dependencies allow.
- **References**: Use `$(ref.my-network.selfLink)` to create dependencies between resources (e.g., VM waiting for Network).

## Exam Focus Areas

1.  **Scenario**: "Need to deploy the EXACT same environment (Dev, Test, Prod) repeatedly." -> **Infrastructure as Code** (Deployment Manager or Terraform).
2.  **Scenario**: "Need to verify what resources will be created before committing." -> **Preview Mode**.
3.  **Dependency**: "Ensure the Database is created before the Application Server." -> Use **References** (`$(ref...)`) in the configuration to enforce ordering.
