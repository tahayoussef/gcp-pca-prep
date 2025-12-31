# Cloud Observability Suite - Comprehensive Guide

## Cloud Logging - Introduction

### Overview
Cloud Logging is a fully managed service that collects, stores, searches, analyzes, and monitors log data and events from GCP and AWS.

**Key Features**:
- Automatic log collection from GCP services
- Centralized log storage and retention
- Real-time log viewing and filtering
- Log-based metrics and alerts
- Integration with Cloud Monitoring

###Types of Logs

**1. Audit Logs** (automatically collected):
- **Admin Activity**: Who did what, where, when (always on, no charge, 400-day retention)
- **Data Access**: Who accessed what data (off by default, chargeable)
- **System Event**: GCP system events (automatic resource changes)
- **Policy Denied**: Requests denied due to security policy violations

**2. Application Logs**:
- Custom logs from applications
- Requires instrumentation (Ops Agent, logging libraries)

**3. Component Logs**:
- Service-specific logs (GKE, App Engine, Cloud Run, etc.)

### Log Storage

**Default Retention**:
- Admin Activity: 400 days
- Data Access: 30 days
- Other logs: 30 days

**Log Buckets**:
- `_Required`: Can't configure or delete
- `_Default`: Customizable retention (1-3650 days)
- Custom buckets: User-created, configurable retention

### Log Query Language

**Basic Query**:
```
resource.type="gce_instance"
severity>="ERROR"
timestamp>="2024-01-01T00:00:00Z"
```

**Common Filters**:
- `severity`: DEBUG, INFO, NOTICE, WARNING, ERROR, CRITICAL, ALERT, EMERGENCY
- `resource.type`: GCP resource type
- `log_id()`: Specific log identifier
- `timestamp`: Time range

**Exam Tip**: Know audit log types - Admin Activity is always on and free; Data Access requires enabling and incurs costs.

---

## Cloud Logging - Exports and Sinks

### Log Sinks

**Purpose**: Route logs to destinations for long-term storage, analysis, or compliance

**Supported Destinations**:
1. **Cloud Logging buckets**: Within Cloud Logging (default)
2. **BigQuery datasets**: For SQL analysis
3. **Cloud Storage buckets**: For archival/compliance
4. **Pub/Sub topics**: For streaming to external systems
5. **Other Google Cloud projects**: Cross-project aggregation

### Sink Configuration

**Components**:
- **Filter**: Which logs to export (inclusion/exclusion)
- **Destination**: Where to send logs
- **Resource scope**: Organization, folder, project, or resource level

**Example Sink Filter**:
```
# Export all ERROR and above from production VMs
resource.type="gce_instance"
resource.labels.environment="production"
severity>=ERROR
```

### Common Patterns

**1. Compliance/Archival**:
```
All logs → Cloud Storage (long-term retention, low cost)
```

**2. Security Analysis**:
```
Audit logs → BigQuery (SQL queries for security investigations)
```

**3. Real-time Processing**:
```
Application logs → Pub/Sub → Dataflow → External SIEM
```

**4. Centralized Logging**:
```
Multiple projects → Aggregation project log bucket
```

### Exports vs. Sinks Distinction

- **Export**: Manual/scheduled export of existing logs
- **Sink**: Real-time routing of logs as they're created (continuous)

**Best Practice**: Use sinks for continuous export; configure at project/org level for consistency

**Exam Tip**: Know export destinations and use cases - BigQuery for analysis, Cloud Storage for archival, Pub/Sub for streaming. Sinks work in real-time.

---

## Cloud Monitoring - Introduction

### Overview
Cloud Monitoring provides visibility into the performance, availability, and health of applications and infrastructure.

**Key Capabilities**:
- Metrics collection and visualization
- Dashboard creation
- Alerting policies
- Uptime monitoring
- Service monitoring (SLOs)

### Monitoring Data Model

**Metric**:
- Time-series data (e.g., CPU utilization over time)
- Identified by metric type (e.g., `compute.googleapis.com/instance/cpu/utilization`)
- Contains labels for filtering (e.g., `instance_id`, `zone`)

**Types of Metrics**:
1. **System metrics**: Auto-collected from GCP services (compute, storage, etc.)
2. **Application metrics**: Custom metrics from applications (via APIs/libraries)
3. **Log-based metrics**: Derived from log entries
4. **Custom metrics**: User-defined via Monitoring API

### Dashboards

**Purpose**: Visualize metrics in a single pane of glass

**Chart Types**:
- Line charts: Time-series trends
- Stacked area: Cumulative values
- Heatmaps: Distribution visualization
- Tables: Tabular data
- Gauges: Current values vs. thresholds

**Best Practices**:
- Group related metrics (e.g., all web server metrics)
- Use filters for specific resources
- Set meaningful time ranges
- Share dashboards with teams

---

## Cloud Monitoring - Uptime Checks

### Overview
Uptime checks proactively monitor the availability and latency of external-facing services.

**Types**:
1. **HTTP/HTTPS**: Check web endpoints
2. **TCP**: Check port availability
3. **Custom**: Monitor any service via synthetic monitoring

### Configuration

**Check Frequency**: Every 1, 5, 10, or 15 minutes

**Check Locations**: Choose from global regions (monitor from multiple locations)

**Response Validation**:
- Status code (e.g., 200 OK)
- Response body content
- SSL certificate validity
- Custom regex patterns

### Alerting on Uptime Checks

**Alert Conditions**:
- Failed from any location
- Failed from X% of locations
- Response time exceeds threshold

**Use Cases**:
- External website availability
- API endpoint monitoring
- Database connection checks
- Load balancer health

**Exam Tip**: Uptime checks monitor external services from multiple global locations - use for public-facing endpoints.

---

## Cloud Monitoring - Mapping Business Objectives to Technical Metrics

### Site Reliability Engineering (SRE) Principles

**Key Concepts**:
- **SLI (Service Level Indicator)**: Quantitative measure of service level (e.g., latency, availability)
- **SLO (Service Level Objective)**: Target value/range for SLI (e.g., 99.9% availability)
- **SLA (Service Level Agreement**): Contract with consequences for missing SLOs
- **Error Budget**: Allowed downtime/errors to balance innovation vs. reliability

### Mapping Process

**1. Identify Business Objectives**:
- "Users should experience fast page loads"
- "Application should be available 24/7"
- "Data should be processed accurately"

**2. Define SLIs** (measurable proxies):
- Page load latency (95th percentile < 200ms)
- Availability (successful requests / total requests)
- Data accuracy (errors per million records)

**3. Set SLOs** (targets):
- 95% of requests complete in < 200ms
- 99.9% availability (43 min downtime/month allowed)
- < 0.001% error rate

**4. Implement Monitoring**:
- Collect SLI metrics (via Cloud Monitoring)
- Track SLO burn rate
- Alert when approaching SLO violation

**Golden Signals** (Google SRE):
1. **Latency**: Request response time
2. **Traffic**: Request volume
3. **Errors**: Failed request rate
4. **Saturation**: Resource utilization (CPU, memory, disk)

**Example Mapping**:
| Business Need | SLI | SLO | Technical Metric |
|---------------|-----|-----|------------------|
| Fast checkout | Request latency (p95) | < 300ms | `http_request_duration_seconds{quantile="0.95"}` |
| Always available | Success rate | 99.95% | `(successful_requests / total_requests) * 100` |
| Scalable | CPU usage | < 75% | `compute.googleapis.com/instance/cpu/utilization` |

**Exam Tip**: Understand SLI/SLO/SLA distinction. Map business goals to measurable SLIs (latency, availability, error rate). Use error budgets to balance reliability vs. velocity.

---

## Cloud Trace

### Overview
Cloud Trace is a distributed tracing system that collects latency data from applications to identify performance bottlenecks.

**Purpose**:
- Understand request flow across microservices
- Identify slow operations/dependencies
- Root cause analysis for latency issues

### Key Concepts

**Trace**: End-to-end journey of a request through the system

**Span**: Individual operation within a trace (e.g., database query, API call, function execution)

**Span Hierarchy**: Parent-child relationships showing call stack

**Latency Analysis**:
- Visualize time spent in each span
- Identify bottlenecks (slowest spans)
- Compare traces over time

### Automatic vs. Manual Instrumentation

**Automatic** (no code changes):
- App Engine
- Cloud Run
- GKE (with Istio/service mesh)

**Manual** (requires SDK):
- Custom applications via OpenTelemetry or Cloud Trace SDK
- Explicit span creation in code

### Use Cases

1. **Microservices debugging**: Trace request across multiple services
2. **Latency investigation**: Find slow database queries, API calls
3. **Dependency mapping**: Understand service interactions
4. **Performance optimization**: Identify critical paths

**Integration**:
- Works with Cloud Logging (correlate logs with traces via trace ID)
- Works with Cloud Profiler (continuous profiling)
- Supports OpenTelemetry standard

**Example**: E-commerce checkout trace:
```
Trace (2.5s total)
├── Web Frontend (50ms)
│   ├── Authentication Service (30ms)
│   └── Authorization Check (20ms)
├── Order Service (100ms)
│   ├── Inventory Check (40ms)
│   └── Order Creation (60ms)
└── Payment Service (2.3s) ← BOTTLENECK
    ├── Payment Gateway API (2.2s)
    └── Transaction Log (100ms)
```

**Exam Tip**: Cloud Trace shows end-to-end request flow and latency breakdown - essential for distributed system debugging. Know it's automatic for App Engine/Cloud Run, manual for custom apps.

---

## Exam Focus Areas

### Critical Concepts

1. **Cloud Logging Components**:
   - **Audit Logs**: Admin Activity (always on, free), Data Access (enable explicitly), System Event, Policy Denied
   - **Retention**: Admin Activity (400 days), others (30 days default, configurable via buckets)
   - **Sinks**: Real-time routing to BigQuery (analysis), Cloud Storage (archival), Pub/Sub (streaming)

2. **Log Export Destinations**:
   | Destination | Use Case | Key Feature |
   |-------------|----------|-------------|
   | Cloud Logging buckets | Default retention | 1-3650 days configurable |
   | BigQuery | Analysis/querying | SQL queries on logs |
   | Cloud Storage | Compliance/archival | Low-cost long-term |
   | Pub/Sub | Streaming | Real-time processing |

3. **Cloud Monitoring**:
   - **Metrics**: Time-series data (system auto-collected, custom via API)
   - **Dashboards**: Visualize metrics
   - **Alerting**: Conditions + notification channels
   - **Uptime Checks**: External endpoint monitoring from global locations

4. **SRE Concepts**:
   - **SLI**: Measurement (e.g., latency, availability)
   - **SLO**: Target (e.g., 99.9% available, p95 latency < 200ms)
   - **SLA**: Contract (SLO with consequences)
   - **Error Budget**: 1 - SLO (e.g., 99.9% = 0.1% allowed errors)
   - **Golden Signals**: Latency, Traffic, Errors, Saturation

5. **Cloud Trace**:
   - Distributed tracing for latency analysis
   - Trace = request, Span = operation
   - Automatic (App Engine, Cloud Run) vs. Manual (SDK)
   - Integrates with logging (trace ID correlation)

### Common Exam Scenarios

- **Scenario**: Retain audit logs for 7 years for compliance
  - **Solution**: Export Admin Activity logs to Cloud Storage via sink (Logging retention max is 3650 days, need external storage)

- **Scenario**: Troubleshoot slow microservices application
  - **Solution**: Enable Cloud Trace, analyze spans to identify bottleneck service

- **Scenario**: Create quarterly cost analysis from logs
  - **Solution**: Export logs to BigQuery via sink, query with SQL

- **Scenario**: Detect when API latency exceeds 500ms
  - **Solution**: Create alerting policy in Cloud Monitoring with latency metric threshold

- **Scenario**: Monitor website availability from multiple continents
  - **Solution**: Configure uptime check with multiple check locations (US, EU, Asia)

- **Scenario**: Define SLO for 99.95% availability
  - **Solution**: SLI = (successful requests / total requests), SLO = 99.95%, Error budget = 0.05% (21.6 min/month)

- **Scenario**: SIEM integration requires real-time log streaming
  - **Solution**: Create log sink to Pub/Sub topic, subscribe external SIEM

---

## Related Services

- **Cloud Profiler**: Continuous CPU/memory profiling
- **Cloud Debugger**: Live debugging of production code
- **Error Reporting**: Aggregate and display errors from logs
- **Cloud Audit Logs**: Built-in audit trail (integrated with Logging)
- **Operations suite**: Umbrella term for Logging, Monitoring, Trace, Profiler, Debugger
- **OpenTelemetry**: Open-source observability framework (supported by GCP)
