# CI/CD - Comprehensive Guide

## Overview
**Continuous Integration (CI)** and **Continuous Delivery (CD)** are essential operational practices on Google Cloud. The primary managed services are **Cloud Build** (CI) and **Cloud Deploy** (CD).

## Cloud Build (CI)
- **Function**: Serverless CI/CD platform. Builds source code, runs tests, and produces artifacts (Docker images, Java archives).
- **Triggers**: Automatically runs builds on git commits, tag pushes, or Pull Requests. Supported repos: Cloud Source Repositories, GitHub, Bitbucket.
- **Build Config**: Defined in `cloudbuild.yaml`. Steps are executed in temporary Docker containers.
- **Worker Pools**:
  - **Default**: Public internet access, ephemeral.
  - **Private Pools**: Access private resources in VPC, custom machine types, static IPs.

## Cloud Deploy (CD)
- **Function**: Managed continuous delivery service for GKE, Cloud Run, and Anthos.
- **Pipelines**: Defines the progression of a release through environments (e.g., `dev` -> `stage` -> `prod`).
- **Features**:
  - **Promotions**: Manual or automated promotion of releases between targets.
  - **Rollbacks**: One-click rollback to a previous stable release.
  - **Approvals**: Gate mechanisms for production deployments.

## Artifact Registry
- **Evolution**: The successor to Container Registry.
- **Storage**: Stores Docker images, Maven/Gradle/npm/Python packages, and OS packages (Debian/RPM).
- **Vulnerability Scanning**: Automatically scans images for known CVEs.

## Exam Focus Areas

1.  **Scenario**: "Need to run unit tests and build a container every time a developer pushes to the `main` branch." -> **Cloud Build Trigger**.
2.  **Scenario**: "Need to access a private database in a VPC during the build process." -> **Cloud Build Private Pools**.
3.  **Scenario**: "Strict compliance requires manual approval before deploying to production." -> **Cloud Deploy** with approval gates.
4.  **Scenario**: "Where to store private Python packages?" -> **Artifact Registry** (Python repository).
