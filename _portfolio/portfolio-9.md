---
title: "Serverless Data Pipeline for Real-Time Analytics"
excerpt: "Architected a fully serverless data platform processing 2.8 billion events daily with 99.99% reliability, enabling real-time dashboards and alerts while reducing infrastructure costs by 73% compared to the previous Spark cluster approach."
collection: portfolio
---

## Project Overview

Designed and implemented a serverless data pipeline for a SaaS company with 23 million active users, replacing their overprovisioned Spark infrastructure. The platform ingests application events, transforms them in real-time, and powers analytics dashboards, ML feature computation, and automated alerting.

## The Challenge

The existing data infrastructure was costly and inflexible:

- **Infrastructure costs:** $1.2M monthly for always-on Spark clusters
- **Utilization:** Average cluster utilization only 23%
- **Latency:** 15-minute minimum for data availability in dashboards
- **Reliability:** Weekly incidents due to cluster management complexity
- **Scalability:** Manual intervention required for traffic spikes
- **Team burden:** 3 FTEs dedicated to cluster operations

Requirements:

- Reduce infrastructure costs by 50%+
- Real-time data availability (<1 minute latency)
- Zero operational overhead for scaling
- 99.9% reliability SLA
- Support 5B events/day peak capacity
- Enable self-service analytics for product teams

## Technical Architecture

### Event Ingestion

**Collection layer:**

- SDK integration in web, iOS, Android applications
- Batched transmission (configurable batch size and interval)
- Client-side retry with exponential backoff
- Offline queuing for network interruptions
- Schema validation at collection point

**Ingestion API:**

- AWS API Gateway with Lambda authorizer
- Request validation and enrichment
- Kinesis Data Streams as buffer
- Multi-region deployment for latency
- Rate limiting and abuse protection

**Scale characteristics:**

- 2.8 billion events/day average
- 5.2 billion events/day peak (Black Friday)
- 47,000 events/second peak throughput
- 99.99% ingestion success rate

### Stream Processing

**Real-time transformation:**
AWS Lambda consumers on Kinesis streams:

```python
# Simplified event processing
def process_event(event):
    # Parse and validate
    parsed = parse_event(event)

    # Enrich with user context
    enriched = enrich_user_data(parsed)

    # Compute derived fields
    transformed = compute_derivatives(enriched)

    # Route to appropriate destinations
    route_event(transformed)
```

**Processing stages:**

1. **Parsing:** Decode and validate event schema
2. **Enrichment:** Add user attributes, session context, geo data
3. **Transformation:** Compute derived metrics, sessionization
4. **Aggregation:** Update real-time counters and rollups
5. **Routing:** Send to appropriate downstream systems

**Lambda configuration:**

- Provisioned concurrency for consistent latency
- Reserved concurrency limits per function
- Error handling with DLQ
- Automatic retry with backoff

### Storage Layer

**Real-time store (hot):**

- Amazon DynamoDB for latest state
- Single-digit millisecond reads
- TTL for automatic expiration
- Global tables for multi-region

**Time-series store (warm):**

- Amazon Timestream for metrics
- Automatic tiering (memory → magnetic)
- SQL query interface
- Built-in analytics functions

**Data lake (cold):**

- S3 with Parquet format
- Partitioned by date and event type
- Iceberg table format for ACID transactions
- 3-year retention with lifecycle policies

### Query Layer

**Real-time dashboards:**

- WebSocket API for live updates
- Lambda functions computing metrics on-demand
- Redis caching for expensive computations
- Pre-aggregated metrics for common queries

**Ad-hoc analytics:**

- Amazon Athena on S3 data lake
- Partition pruning for query efficiency
- Query result caching
- Workgroup-based cost allocation

**Embedded analytics:**

- QuickSight embedded dashboards
- Row-level security based on customer
- Scheduled reports to email
- Export to CSV/Excel

### Alerting and Automation

**Metric monitoring:**

- CloudWatch metrics from Lambda
- Custom metrics published from processing
- Composite alarms for complex conditions
- SNS for alert distribution

**Anomaly detection:**

- Statistical baseline computation
- Real-time comparison to baseline
- Automatic threshold adjustment
- Seasonality awareness (hourly, daily, weekly)

**Automated actions:**

- Lambda-triggered remediation
- Slack/PagerDuty integration
- Automated runbook execution
- Customer notification workflows

## Cost Optimization

### Pay-per-use Model

**Before (Spark cluster):**

```
EMR cluster (always-on): $890,000/month
S3 storage: $145,000/month
Data transfer: $165,000/month
---
Total: $1,200,000/month
```

**After (serverless):**

```
Lambda execution: $47,000/month
Kinesis: $23,000/month
DynamoDB: $89,000/month
S3 + Athena: $112,000/month
Other services: $52,000/month
---
Total: $323,000/month
```

**Savings: $877,000/month (73%)**

### Optimization Techniques

**Lambda:**

- Right-sized memory allocation (power tuning)
- ARM64 architecture (Graviton2)
- Provisioned concurrency only where needed
- Code optimization for cold start reduction

**DynamoDB:**

- On-demand capacity for variable workloads
- DAX caching for read-heavy patterns
- TTL to reduce storage costs
- Efficient key design to minimize read costs

**S3:**

- Intelligent tiering for uncertain access patterns
- Lifecycle policies for automatic transitions
- Parquet compression reducing storage 8x
- Athena query optimization reducing scan costs

## Reliability Engineering

### Fault Tolerance

**Kinesis resilience:**

- Multi-AZ data replication
- 7-day retention for replay capability
- Enhanced fan-out for parallel consumers
- Dead letter queue for failed records

**Lambda resilience:**

- Automatic retry with backoff
- Function-level error handling
- Circuit breaker pattern for dependencies
- Fallback to degraded mode

**Cross-region:**

- Active-passive configuration
- Route 53 health checks
- Automated failover
- Data replication via S3 CRR

### Observability

**Metrics:**

- CloudWatch dashboards for operations
- Custom metrics for business KPIs
- X-Ray tracing for latency analysis
- Contributor Insights for debugging

**Logging:**

- Structured JSON logging
- CloudWatch Logs with Insights
- Log retention policies
- Automated error detection

**Alerting:**

- PagerDuty integration
- Escalation policies
- Runbook links in alerts
- Post-incident automation

## Results

### Performance Metrics

| Metric                  | Before     | After       |
| ----------------------- | ---------- | ----------- |
| Data latency            | 15 minutes | 47 seconds  |
| Ingestion reliability   | 99.7%      | 99.99%      |
| Query performance (p50) | 12 seconds | 1.8 seconds |
| Dashboard refresh       | Manual     | Real-time   |
| Incident frequency      | Weekly     | Monthly     |

### Operational Improvements

| Metric                         | Before | After              |
| ------------------------------ | ------ | ------------------ |
| Infrastructure management FTEs | 3      | 0.5                |
| Deployment frequency           | Weekly | Multiple daily     |
| Scaling intervention           | Manual | Automatic          |
| Cost variability               | Fixed  | Usage-proportional |

### Business Impact

**Cost savings:**

- Annual infrastructure savings: $10.5M
- Team reallocation to product work: 2.5 FTEs

**Product improvements:**

- Real-time analytics enabled new features
- Customer-facing dashboards with live data
- Proactive alerting reduced customer-reported issues 67%

**Developer productivity:**

- Self-service data access for product teams
- Schema evolution without downtime
- Experimentation with new metrics cost-effective

## Technologies Used

- **Ingestion:** API Gateway, Kinesis Data Streams
- **Processing:** AWS Lambda (Python, Node.js)
- **Storage:** DynamoDB, Timestream, S3, Iceberg
- **Query:** Athena, QuickSight
- **Observability:** CloudWatch, X-Ray
- **Infrastructure:** Terraform, AWS CDK
- **CI/CD:** GitHub Actions, AWS SAM

## Lessons Learned

**Serverless isn't zero-ops:**

- Observability requires investment
- Cost monitoring essential
- Capacity planning still needed (limits exist)
- Debugging distributed systems is hard

**Design for failure:**

- Every component will fail eventually
- DLQ and retry logic from day one
- Idempotency in all transformations
- Graceful degradation over hard failure

**Start simple, optimize later:**

- Initial design was intentionally naive
- Profiled production before optimizing
- Optimizations based on data, not intuition
- Cost optimization ongoing, not one-time

## Links

- [Architecture Documentation](#)
- [Runbook](#)
- [Cost Analysis](#)
- [Migration Guide](#)

