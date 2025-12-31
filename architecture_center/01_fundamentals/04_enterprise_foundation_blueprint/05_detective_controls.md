# Detective Controls (Enterprise Foundation Blueprint)

## Overview
Detective controls provide visibility into your environment, enabling you to detect misconfigurations, vulnerabilities, and active threats. The blueprint establishes a centralized logging and monitoring architecture.

## Architecture Components

### Centralized Logging
*   **Aggregation**: All logs from the organization are routed to a central project (`prj-c-logging`) using **Log Sinks**.
*   **Log Types**: 
    *   **Admin Activity & System Event**: Mandatory audit logs.
    *   **VPC Flow Logs**: Enabled for all subnets (at 50% sampling) to track network traffic.
    *   **Firewall Rules Logging**: Enabled for all rules.
    *   **DNS Logging**: Enabled for managed zones.

### Security Command Center (SCC)
SCC is the primary dashboard for threat detection.
*   **Security Health Analytics (SHA)**: Detects misconfigurations (e.g., public bucket).
*   **Event Threat Detection (ETD)**: analyzes logs for suspicious patterns (e.g., malware, cryptomining).
*   **Integration**: Findings are exported to Pub/Sub (`prj-c-scc`) for integration with external SIEMs (Splunk, QRadar, Google SecOps) or remediation workflows.

### Automated Log Analysis
For custom alerting needs beyond SCC:
*   **Solution**: Export logs to **BigQuery** and use scheduled queries (Cloud Run/Functions) to scan for specific business-logic violations or high-risk events (e.g., Super Admin logins).
*   **Alerting**: Generate custom findings in SCC or send notifications via Pub/Sub.
