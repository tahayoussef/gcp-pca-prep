# Generative AI Knowledge Base (Jump Start Solution)

## Overview
Deploy a ready-to-use application that extracts question-and-answer pairs from documents and trains a prompt-based model.

## Objectives
*   Extract Q&A pairs from uploaded documents.
*   Deploy a pipeline triggered by document uploads.
*   Train a prompt-based AI model using extracted Q&A data.

## Architecture
*   Event-driven pipeline automatically processes documents in Cloud Storage.
*   Uses **Vertex AI Generative AI** and LLMs.
*   Can be deployed via **Console** or **Terraform CLI**.

## Use Case
*   Build domain-specific knowledge bases from existing documentation.
*   Tune LLM for organization-specific Q&A.
