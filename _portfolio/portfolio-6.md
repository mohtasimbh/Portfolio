---
title: "Real-Time Fraud Detection Engine for Digital Payments"
excerpt: "Built a machine learning-powered fraud detection system processing 23,000 transactions per second with sub-50ms latency, blocking $127M in annual fraud while maintaining 99.7% legitimate transaction approval rate and adapting to emerging fraud patterns in real-time."
collection: portfolio
---

## Project Overview

Developed an enterprise fraud detection platform for a major payment processor handling 2 billion transactions monthly. The system evaluates every transaction in real-time, applying hundreds of rules and ML models to distinguish legitimate purchases from fraud, while minimizing false positives that frustrate customers.

## The Challenge

The client faced escalating fraud losses and customer friction:

- **Fraud losses:** $156M annually in chargebacks and fraud reimbursements
- **False positives:** 3.2% of legitimate transactions declined, causing $89M in lost revenue
- **Customer friction:** Average of 4.7 unnecessary challenges per customer annually
- **Detection latency:** 340ms average decision time, causing checkout abandonment
- **Adaptability:** New fraud patterns took 6-8 weeks to address with rule updates
- **Regulatory pressure:** PSD2 SCA requirements demanding risk-based authentication

Requirements:

- Process 25,000+ transactions per second at peak
- Decision latency under 50ms (p99)
- Reduce fraud losses by 40%+ without increasing false positives
- Adapt to new patterns within hours, not weeks
- Support explainable decisions for regulatory compliance
- Handle multiple payment types (card-present, card-not-present, ACH, real-time payments)

## Technical Architecture

### Real-Time Decision Engine

**Transaction flow:**

1. Transaction received via API gateway
2. Feature enrichment from multiple sources (parallel)
3. Rule engine evaluation
4. ML model inference
5. Score aggregation and decision
6. Response returned to merchant

**All within 50ms budget.**

**Feature enrichment:**
Parallel lookups to enrich raw transaction with context:

_Customer features:_

- Historical transaction patterns (velocity, typical amounts, merchants)
- Device fingerprint matching
- Behavioral biometrics (if available)
- Account age and history

_Merchant features:_

- Merchant risk profile
- Industry-specific fraud rates
- Historical chargeback rates
- Geographic risk factors

_Transaction features:_

- Distance from last transaction
- Time since last transaction
- Amount deviation from typical
- Cross-border indicators

_External data:_

- BIN database (card issuer, country, type)
- IP geolocation and proxy detection
- Email reputation scores
- Phone number verification

**Low-latency data stores:**

- Redis Cluster for customer profiles (sub-millisecond reads)
- Aerospike for historical patterns (P99 < 1ms)
- In-memory feature cache with background refresh
- Fallback defaults when lookups timeout

### Rule Engine

**Velocity rules:**

- Transaction count limits (per hour, day, week)
- Amount thresholds (single and cumulative)
- Unique merchant/country/device counts
- Configurable by customer segment

**Pattern rules:**

- Geographic impossibility (two countries within impossible time)
- Card testing patterns (small amounts, sequential failures)
- Known fraud indicators (high-risk MCCs, BINs)
- Anomaly thresholds from ML models

**Rule management:**

- Business users configure rules via UI
- Version control for all changes
- A/B testing framework for new rules
- Automatic rollback on performance degradation

### Machine Learning Models

**Model ensemble:**
Multiple specialized models combined for robust detection:

_Gradient boosting (primary):_

- XGBoost trained on 2 years of labeled transactions
- 847 features including engineered and raw
- Updated weekly with new fraud patterns
- Fast inference (<5ms)

_Neural network (patterns):_

- LSTM for sequential transaction patterns
- Captures behavioral anomalies
- Particularly effective for account takeover
- Runs asynchronously with timeout

_Isolation forest (anomalies):_

- Unsupervised detection of novel patterns
- Catches attacks not seen in training
- Low precision but valuable signal
- Helps identify emerging fraud types

_Graph neural network (networks):_

- Detects coordinated fraud rings
- Models relationships between cards, devices, merchants
- Runs offline, features served in real-time
- Particularly effective for bust-out fraud

**Score aggregation:**

```python
final_score = (
    0.45 * xgboost_score +
    0.25 * lstm_score +
    0.15 * isolation_score +
    0.10 * gnn_score +
    0.05 * rule_score
)
```

Weights tuned through A/B testing on live traffic.

**Model training pipeline:**

- Daily retraining with new labeled data
- Champion/challenger model deployment
- Automatic promotion based on performance metrics
- Canary rollout (1% → 10% → 50% → 100%)
- Rollback triggers on KPI degradation

### Adaptive Learning

**Feedback loops:**

- Confirmed fraud (chargebacks) labeled within 24 hours
- Confirmed legitimate (successful delivery) labeled within 7 days
- Manual review labels incorporated immediately
- Velocity of feedback incorporation: 4 hours

**Emerging pattern detection:**

- Clustering on declined transactions to find new attack vectors
- Anomaly detection on model confidence distributions
- Automatic alert when novel patterns exceed threshold
- Rapid rule deployment for immediate mitigation

**Continuous model updating:**

- Online learning layer for immediate adaptation
- Full retraining for structural pattern changes
- Feature importance monitoring for drift detection
- Automatic retraining triggered by performance degradation

### Explainability

**Decision reasons:**
Every decision includes human-readable explanations:

- Top contributing factors (SHAP values)
- Triggered rules with descriptions
- Comparison to typical customer behavior
- Confidence level and recommendation

**Regulatory compliance:**

- Full audit trail for every decision
- Customer dispute support with explanation retrieval
- Analyst investigation tools
- GDPR-compliant data handling

**Analyst tools:**

- Case management interface
- Similar transaction lookup
- Customer history visualization
- Rule simulation sandbox

## Infrastructure

### High-Availability Design

**Compute:**

- Kubernetes deployment across 3 availability zones
- Active-active configuration
- Automatic pod scaling based on queue depth
- Reserved capacity for peak periods

**Data stores:**

- Redis Cluster with replication
- Aerospike with strong consistency
- Multi-region replication for DR
- Automatic failover tested weekly

**Traffic management:**

- Geographic load balancing
- Health-check based routing
- Circuit breakers for degraded dependencies
- Graceful degradation with cached decisions

### Performance Optimization

**Latency budget allocation:**
| Component | Budget | Actual (P99) |
|-----------|--------|--------------|
| Network/routing | 5ms | 3.2ms |
| Feature enrichment | 20ms | 16.8ms |
| Rule evaluation | 5ms | 2.1ms |
| ML inference | 15ms | 11.4ms |
| Response | 5ms | 2.9ms |
| **Total** | **50ms** | **36.4ms** |

**Optimizations applied:**

- Feature lookups parallelized
- Model compiled with ONNX Runtime
- Connection pooling for all external calls
- Aggressive timeout management
- Hot-path code profiled and optimized

### Monitoring

**Real-time dashboards:**

- Transaction throughput and latency
- Fraud rate and false positive rate
- Model performance metrics
- System health indicators

**Alerting:**

- Latency degradation
- Error rate spikes
- Fraud rate anomalies
- Model drift detection

**Analytics:**

- Fraud pattern analysis
- Customer segment performance
- Merchant risk profiling
- Attack vector trending

## Results

### Detection Performance

| Metric                  | Before    | After     |
| ----------------------- | --------- | --------- |
| Fraud detection rate    | 67%       | 91%       |
| False positive rate     | 3.2%      | 0.9%      |
| Decision latency (P99)  | 340ms     | 47ms      |
| Emerging fraud response | 6-8 weeks | 4-6 hours |

### Business Impact

**Fraud reduction:**

- Annual fraud losses reduced from $156M to $54M
- Net fraud savings: $102M annually
- Detection rate improved 36% (67% → 91%)

**Customer experience:**

- False positive rate reduced 72% (3.2% → 0.9%)
- Recovered revenue from prevented false declines: $67M
- Customer friction events reduced 81%

**Operational efficiency:**

- Manual review volume reduced 63%
- Analyst productivity improved 4.2x
- Time to address new fraud patterns: 6 weeks → 4 hours

### ROI

- Platform investment: $8.2M
- Annual benefit: $169M (fraud savings + recovered revenue + efficiency)
- Payback period: 18 days

## Technologies Used

- **Real-Time Processing:** Apache Kafka, Apache Flink
- **Storage:** Redis Cluster, Aerospike, PostgreSQL
- **ML Platform:** MLflow, ONNX Runtime, XGBoost, PyTorch
- **Rule Engine:** Custom Rust implementation
- **Infrastructure:** Kubernetes, Istio, AWS
- **Monitoring:** Prometheus, Grafana, custom dashboards
- **Languages:** Python, Rust, Go

## Lessons Learned

**Latency is a feature:**

- Every millisecond of latency costs merchant conversion
- Invested heavily in optimization from day one
- Parallel processing essential for feature enrichment
- Timeout handling as important as happy path

**False positives matter more than detection:**

- Customers remember declined transactions
- Merchants leave over excessive friction
- Precision often more valuable than recall
- Segment-specific thresholds essential

**Fraud evolves continuously:**

- Static models decay within weeks
- Investment in adaptability, not just accuracy
- Feedback loops are infrastructure, not nice-to-have
- Anomaly detection catches what supervised learning misses

## Links

- [Technical Architecture](#)
- [Model Performance Metrics](#)
- [Integration Guide](#)
- [Analyst User Guide](#)

```

---
```
