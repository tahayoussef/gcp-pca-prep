# App Development with Deployment Pipeline (Jump Start Solution)

## Overview
End-to-end CI/CD pipeline for app development using **Cloud Code**, **Cloud Build**, and **GKE**.

## Components
*   **Cloud Code**: IDE extension for developing Kubernetes apps.
*   **Cloud Build**: CI/CD pipeline (build, test, deploy).
*   **Cloud Deploy**: Progressive delivery to GKE.
*   **GKE**: Runtime environment.

## Workflow
1.  Developer writes code using Cloud Code.
2.  Commit triggers Cloud Build pipeline.
3.  Cloud Build builds container, runs tests.
4.  Cloud Deploy deploys to GKE (dev → staging → prod).
