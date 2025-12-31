# Generative AI Document Summarization (Jump Start Solution)

## Overview
Deploy a ready-to-use application that automatically summarizes uploaded PDF documents.

## Objectives
*   Understand how the document summarization application works.
*   Deploy orchestration for the summarization process.
*   Trigger pipeline with PDF upload and view generated summary.

## Architecture
*   **Cloud Storage**: PDF upload.
*   **Eventarc**: Triggers processing.
*   **Cloud Run Functions**: Orchestrates workflow.
*   **Document AI**: Parses PDF.
*   **Vertex AI Generative AI**: Generates summary.
*   **BigQuery**: Stores results.

## Deployment
*   Deploy via **Console** or **Terraform CLI**.
*   Event-driven, serverless architecture.
