# Deploy the Blueprint

## Overview
Deployment options and steps for the Enterprise Application Blueprint.

## Deployment Options

###Option 1: New Organization
*   Deploy Enterprise Foundation Blueprint first.
*   Then deploy Enterprise Application Blueprint on top.
*   Full reference implementation with all security controls.

### Option 2: Without Enterprise Foundation
*   Deploy blueprint standalone (not recommended for production).
*   Missing enterprise-level security and organizational structure.

### Option 3: Incorporate into Existing GKE
*   Adapt blueprint components to existing GKE deployment.
*   Selective adoption of patterns and practices.

## Deployment Steps
1.  **Prerequisites**: Enterprise Foundation Blueprint (recommended).
2.  **Infrastructure Pipeline**: Deploy multi-tenant platform infrastructure.
3.  **Fleet & App Factory**: Set up fleet management and application CI/CD.
4.  **Deploy Cymbal Bank**: Reference app deployment for validation.

## Customization
*   Blueprint provides defaults; customize as needed (machine types, regions, policies).
