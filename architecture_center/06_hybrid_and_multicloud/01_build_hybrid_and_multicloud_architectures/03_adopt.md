# Adopt Hybrid and Multicloud Architecture

## Overview
Architectural approaches for cloud adoption and migration.

## Migration Approaches

### 1. Lift and Shift (Rehost)
*   Move VMs as-is to cloud.
*   Fastest migration; minimal code changes.
*   Limited cloud-native benefits.

### 2. Replatform
*   Minor modifications to leverage managed services (e.g., use Cloud SQL instead of self-managed DB).
*   Balance speed and cloud benefits.

### 3. Refactor/Re-architect
*   Redesign apps for cloud-native (containers, microservices, serverless).
*   Maximum cloud benefits; most effort.

### 4. Hybrid Approach
*   Keep some workloads on-prem; move others to cloud.
*   Gradual transition.

## Cloud-First Principle
*   **Default to Cloud**: Unless constraints require on-prem, deploy new workloads to cloud.
*   **Exceptions**: Regulatory, latency, legacy dependencies.

## Mix and Match
*   Different workloads may use different approaches.
*   Start with lift-and-shift for quick wins; refactor over time.
