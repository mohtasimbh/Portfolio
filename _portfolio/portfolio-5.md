---
title: "Predictive Maintenance System for Industrial IoT"
excerpt: "Developed an end-to-end predictive maintenance platform analyzing sensor data from 12,000 industrial machines, achieving 94% accuracy in failure prediction 72 hours in advance, reducing unplanned downtime by 67% and maintenance costs by $4.2M annually."
collection: portfolio
---

## Project Overview

Created a comprehensive predictive maintenance solution for a global manufacturing conglomerate operating across 23 facilities worldwide. The system ingests real-time sensor data from industrial equipment, applies machine learning models to predict failures, and integrates with maintenance management systems to automate work order generation.

## The Challenge

The client operated critical manufacturing equipment with significant costs associated with failures:

- **Unplanned downtime:** Average 847 hours monthly across all facilities, costing $127K per hour
- **Reactive maintenance:** 73% of maintenance was reactive (fix after failure)
- **Spare parts inventory:** $34M tied up in "just in case" inventory
- **Safety incidents:** 12 injuries annually related to equipment failures
- **Maintenance scheduling:** Inefficient time-based maintenance regardless of actual condition

Goals for the new system:

- Predict failures 48-72 hours in advance with >90% accuracy
- Reduce unplanned downtime by 50%
- Enable condition-based maintenance
- Optimize spare parts inventory
- Integrate with existing SAP PM and SCADA systems
- Deploy across diverse equipment types (CNC machines, conveyors, HVAC, compressors)

## Technical Architecture

### Data Collection Layer

**Sensor infrastructure:**

- 847,000 sensors across 12,000 machines
- Sensor types: vibration, temperature, pressure, current, flow, acoustic
- Sampling rates: 1 Hz (temperature) to 50 kHz (vibration)
- Edge gateways aggregating and preprocessing data
- Industrial protocols: Modbus, OPC-UA, MQTT, Profinet

**Edge processing:**

- NVIDIA Jetson devices at each facility
- Local preprocessing: filtering, downsampling, feature extraction
- Anomaly detection at edge for immediate alerts
- Data compression (10:1) for efficient transmission
- Store-and-forward for connectivity resilience

**Data ingestion:**

- Apache Kafka for real-time streaming
- Kafka Connect for protocol adaptation
- Schema Registry for data governance
- Exactly-once semantics for data integrity

### Data Platform

**Time-series storage:**

- TimescaleDB for structured sensor data
- Configurable retention policies (hot/warm/cold)
- Continuous aggregations for dashboard queries
- Compression achieving 20:1 for historical data

**Feature store:**

- Feast for ML feature management
- Offline store for training (Parquet on S3)
- Online store for inference (Redis)
- Point-in-time correct feature retrieval
- Feature versioning and lineage

**Data lake:**

- Delta Lake for raw data preservation
- Schema evolution handling
- Time travel for reproducibility
- GDPR-compliant data retention

### Machine Learning Pipeline

**Feature engineering:**
Extensive domain-specific feature extraction:

_Time domain:_

- Statistical moments (mean, variance, skewness, kurtosis)
- Peak-to-peak amplitude
- RMS values
- Crest factor

_Frequency domain:_

- FFT-based spectral features
- Dominant frequencies and harmonics
- Spectral entropy
- Band power in characteristic ranges

_Time-frequency:_

- Wavelet decomposition features
- Short-time Fourier transform
- Hilbert-Huang transform for non-stationary signals

_Cross-sensor:_

- Correlation between related sensors
- Phase relationships
- Causal relationships (Granger causality)

**Model architecture:**
Ensemble approach combining multiple techniques:

_LSTM networks:_

- Capture long-term temporal dependencies
- Separate models for each equipment class
- Attention mechanisms for interpretability

_Gradient boosting:_

- XGBoost on engineered features
- Fast inference for real-time scoring
- Feature importance for explainability

_Isolation forests:_

- Unsupervised anomaly detection
- Novel failure mode discovery
- Complement to supervised models

_Survival analysis:_

- Remaining useful life estimation
- Cox proportional hazards model
- Weibull distribution fitting

**Model training:**

- MLflow for experiment tracking
- Hyperparameter optimization with Optuna
- Cross-validation respecting temporal ordering
- Class imbalance handling (SMOTE, class weights)
- Regular retraining with new failure data

**Inference pipeline:**

- Real-time scoring every 5 minutes
- Batch predictions for maintenance planning
- A/B testing framework for model updates
- Automatic fallback on model degradation

### Alert and Integration

**Alert management:**

- Risk scoring on 0-100 scale
- Configurable thresholds by equipment criticality
- Alert routing based on severity and equipment
- Escalation procedures for unacknowledged alerts
- Mobile app for maintenance technicians

**SAP PM integration:**

- Automatic work order creation
- Parts list attachment based on predicted failure mode
- Scheduling optimization considering production plans
- Completion feedback loop for model improvement

**Visualization:**

- Grafana dashboards for operations
- PowerBI for executive reporting
- Custom React application for maintenance planners
- Mobile-responsive design for floor use

## Deployment

### Rollout Strategy

**Pilot phase (3 months):**

- Single facility, 40 critical machines
- Model validation against actual failures
- Process integration with maintenance team
- Threshold tuning based on feedback

**Expansion phase (6 months):**

- Roll out to 8 facilities
- Equipment class coverage expansion
- Integration refinements
- Training for all maintenance teams

**Global deployment (6 months):**

- Remaining facilities
- 24/7 support model establishment
- Continuous improvement process
- Center of excellence creation

### Infrastructure

**Cloud architecture:**

- AWS primary deployment
- Multi-region for global facilities
- Edge-cloud hybrid for low latency
- VPN connectivity to plant networks

**Reliability:**

- 99.9% platform availability
- Graceful degradation during cloud outages
- Local alerting continues independently
- Disaster recovery with 4-hour RTO

## Results

### Prediction Performance

| Equipment Type | Accuracy | Precision | Recall | Lead Time |
| -------------- | -------- | --------- | ------ | --------- |
| CNC Machines   | 94.2%    | 89.1%     | 91.7%  | 73 hours  |
| Conveyors      | 91.8%    | 86.3%     | 88.9%  | 68 hours  |
| Compressors    | 96.1%    | 92.4%     | 94.2%  | 82 hours  |
| HVAC Systems   | 89.4%    | 84.7%     | 86.1%  | 54 hours  |
| Pumps          | 93.7%    | 88.9%     | 90.3%  | 71 hours  |

### Business Impact

**Downtime reduction:**

- Unplanned downtime reduced 67% (847 hours → 280 hours monthly)
- Production availability increased from 91.2% to 97.8%
- Estimated annual value: $8.7M

**Maintenance efficiency:**

- Reactive maintenance reduced from 73% to 24%
- Wrench time improved 34% (less diagnosis, more repair)
- Overtime reduced 42%

**Inventory optimization:**

- Spare parts inventory reduced 28% ($9.4M freed)
- Stockout incidents reduced 89%
- Just-in-time parts ordering enabled

**Safety improvements:**

- Equipment-related injuries reduced from 12 to 2 annually
- Near-miss events reduced 61%

### ROI

- Total investment: $3.2M (platform + deployment + training)
- Annual savings: $12.4M (downtime + maintenance + inventory)
- Payback period: 3.1 months
- 5-year NPV: $47M

## Technologies Used

- **Data Ingestion:** Apache Kafka, Kafka Connect, MQTT
- **Storage:** TimescaleDB, Delta Lake, Redis
- **ML Platform:** MLflow, Feast, Optuna
- **Models:** PyTorch, XGBoost, scikit-learn
- **Processing:** Apache Spark, Dask
- **Orchestration:** Apache Airflow, Kubernetes
- **Visualization:** Grafana, PowerBI, React
- **Edge:** NVIDIA Jetson, AWS Greengrass

## Lessons Learned

**Domain expertise is critical:**

- Partnered with reliability engineers from day one
- Their feature ideas outperformed automated feature engineering
- Physical understanding guided model architecture
- Ongoing collaboration for model refinement

**Start with the business process:**

- Technology is easy; process change is hard
- Early maintenance team involvement built trust
- Workflow integration before algorithm optimization
- Celebrate early wins to build momentum

**Data quality over quantity:**

- Labeled failure data was scarce and precious
- Invested heavily in failure forensics for labeling
- Synthetic data helped but couldn't replace real failures
- Feedback loops from maintenance essential

## Links

- [Technical Architecture](#)
- [Model Performance Reports](#)
- [ROI Analysis](#)
- [Deployment Playbook](#)

```

---
```
