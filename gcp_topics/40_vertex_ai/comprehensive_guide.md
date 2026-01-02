# Vertex AI - Comprehensive Guide

## Overview
Unified MLOps platform for building, deploying, and scaling ML models.
- **Legacy**: Replaces "Cloud AI Platform" and "AutoML".
- **Goal**: Full lifecycle management (Data -> Train -> Deploy -> Monitor).

---

## Core Components

### 1. Training
- **AutoML**: Train high-quality models *without code*.
  - Upload data (Images, Text, Tabular) -> Google trains the model.
- **Custom Training**: Bring your own code (TensorFlow, PyTorch, Scikit-learn).
  - **Pre-built Containers**: Use Google's standard environments.
  - **Custom Containers**: Docker images with any dependencies.

### 2. Vertex AI Pipelines
- **MLOps**: Orchestrate ML workflows using **Kubeflow Pipelines** or **TFX**.
- **Serverless**: No clusters to manage.
- **Structure**: Directed Acyclic Graph (DAG) of steps (Prepare Data -> Train -> Evaluate -> Deploy).

### 3. Feature Store
- **Problem**: "Training team calculated 'User Average Spend', but Serving team re-calculated it differently."
- **Solution**: A central repo for features.
  - **Online Serving**: Low latency (Bigtable/Redis backend) for real-time predictions.
  - **Offline Serving**: High throughput (BigQuery) for batch training.

### 4. Model Garden & Generative AI
- **Model Garden**: Library of Foundation Models (Palm, Gemini, Llama, Claude/Anthropic).
- **Vertex AI Studio**: UI to test prompts and fine-tune LLMs.

---

## Deployment & Prediction
- **Endpoints**: HTTPS endpoints to serve predictions.
- **Traffic Splitting**: Canary deployments (90% to v1, 10% to v2).
- **Explainable AI (XAI)**:
  - "Why did the model reject this loan?"
  - Returns **Feature Attributions** (e.g., "Salary was too low").

---

## Exam Focus Areas

1.  **AutoML vs Custom**:
    - "No data science expertise, need high quality model". -> **AutoML**.
    - "Need full control over network architecture". -> **Custom Training**.

2.  **Dataset Management**:
    - **Vertex AI Managed Datasets**: Unified view of data (Images, Video, Text, Tabular).
    - **Feature Store**: Use for **sharing features** across teams and ensuring **training-serving skew** doesn't happen.

3.  **Pipelines**:
    - "Automate retraining when new data arrives". -> **Vertex AI Pipelines**.

4.  **Hardware**:
    - **TPU (Tensor Processing Unit)**: Best for massive Matrix multiplication (Deep Learning/TensorFlow).
    - **GPU**: General purpose acceleration.
