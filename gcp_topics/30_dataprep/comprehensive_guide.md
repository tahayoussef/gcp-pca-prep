# Cloud Dataprep by Trifacta - Comprehensive Guide

## Overview
Visual tool for cleaning and preparing data for data analysis.
- **Serverless**: Fully managed (uses Dataflow behind the scene).
- **Target Audience**: Business Analysts (No-code/Low-code), Data Scientists.
- **Output**: Exports to BigQuery, GCS, Dataflow.

## Key Concepts
- **Flow**: A container for datasets and recipes.
- **Recipe**: A sequence of transformation steps (Split, Merge, Format, Filter).
- **Wrangler**: The visual interface where you interactively transform data.
- **Job**: When you run a recipe, Dataprep spawns a **Dataflow** job to process the full dataset at scale.

## Exam Focus Areas (Low Priority)
- **Use Case**: "Business analyst needs to identify data quality issues and fix them visually".
- **Integration**: "Clean data before loading into BigQuery".
- **Anomaly Detection**: Built-in visual histograms to spot outliers.
