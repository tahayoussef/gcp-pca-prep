# Application Integration - Comprehensive Guide

## Overview
**Application Integration** is Google Cloud's cloud-native **Integration-Platform-as-a-Service (iPaaS)** solution. It allows you to create integration flows that connect applications (SaaS, custom) and Google Cloud services without writing code.

## Key Features
- **Visual Editor**: Drag-and-drop interface to design flows.
- **Connectors**: Pre-built connectors for Salesforce, ServiceNow, Oracle, BigQuery, Pub/Sub, etc.
- **Triggers**: Event-driven execution (API call, Pub/Sub message, Schedule).
- **Data Mapping**: Visual mapper to transform data structures (JSON -> XML, Field A -> Field B).

## Exam Focus Areas

1.  **Use Case - SaaS to GCP**:
    - "When a new lead is added to **Salesforce**, automatically insert a row into **BigQuery** and notify a **Slack** channel." -> Use **Application Integration**.

2.  **Comparison**:
    - **Application Integration**: Enterprise iPaaS, drag-and-drop, complex flows, SaaS connectors.
    - **Workflows**: Orchestration of GCP services, YAML-based, lower level logic.
    - **Eventarc**: Event routing (Event -> Destination), simpler than full integration logic.
    - **Dataflow**: Heavy ETL/Data processing pipelines (not app integration).

3.  **Key Benefit**:
    - **No-Code/Low-Code**: Speed of development for business process integration.
