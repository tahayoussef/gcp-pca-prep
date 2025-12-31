# Data Science with R on Google Cloud: Exploratory Data Analysis

## Overview
Perform **exploratory data analysis (EDA)** using **R** on **Vertex AI Workbench** with **BigQuery** data.

## Architecture
*   **Vertex AI Workbench**: Managed JupyterLab environment with R kernel.
*   **BigQuery**: Data warehouse for large datasets.
*   **R Libraries**: `bigrquery`, `ggplot2`, `dplyr` for data manipulation and visualization.
*   **Cloud Storage**: Store intermediate results and exports.

## Workflow
1.  **Setup Environment**: Create Vertex AI Workbench instance with R.
2.  **Connect to BigQuery**: Use `bigrquery` package to query BigQuery from R.
3.  **Query Data**: SQL queries executed from R; results loaded into R data frames.
4.  **Exploratory Analysis**:
    *   Summarize data (mean, median, distributions).
    *   Visualize data with `ggplot2`.
    *   Identify patterns, outliers, correlations.
5.  **Process in BigQuery**: Leverage BigQuery for heavy transformations (aggregations, joins).
6.  **Export Results**: Save processed data to CSV in Cloud Storage for further analysis or ML training.

## Benefits
*   **Scalability**: BigQuery handles large datasets; R used for visualization and statistical analysis.
*   **Familiar Tools**: R users can leverage familiar syntax and libraries.
*   **Cost-Effective**: Pay only for BigQuery queries and Workbench runtime.

## Use Cases
*   **Statistical Analysis**: Complex statistical models in R on BigQuery data.
*   **Data Visualization**: Rich visualizations with R libraries.
*   **ML Feature Engineering**: Prepare data in R for ML training.
