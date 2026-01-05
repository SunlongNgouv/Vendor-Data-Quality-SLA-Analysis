## Vendor Data Quality & SLA Monitoring Framework
#### 📌 Project Overview

This project demonstrates a lightweight, scalable framework for evaluating and monitoring third-party data vendors using standardized data quality metrics, SLA monitoring, and side-by-side vendor bake-offs.

The goal is to enable data-driven vendor decisions, improve downstream reliability, and maintain a clear audit trail for compliance and internal transparency.

#### 🎯 Objectives

1. Define a clear, measurable definition of Data Quality
2. Compare multiple vendors using quantitative bake-off metrics
3. Monitor SLA performance and identify breaches early
4. Translate business requirements into technical evaluation logic
5. Provide transparent documentation for audits and stakeholder alignment

#### 🗂️ Project Structure
````
vendor-data-quality/
├── README.md
├── data/
│   ├── vendor_a.csv
│   ├── vendor_b.csv
│   ├── united_states.csv
├── models/
│   ├── Exploratory_data.ipynb
├── docs/
│   ├── data_quality_definition.md
│   ├── vendor_bakeoff_methodology.md
│   └── data_lineage.md
````

#### 📊 Data Model (Mock Vendor Records)

Each vendor provides criminal record-like datasets with the following schema:

| Column      | Description                  |
| ----------- | ---------------------------- |
| record_id   | Unique record identifier     |
| vendor      | Data provider name           |
| county      | Jurisdiction                 |
| dob         | Date of birth (PII)          |
| ssn         | Social Security Number (PII) |
| disposition | Case outcome                 |
| record_date | Source record timestamp      |
| ingest_time | Time data was ingested       |


Mock data intentionally includes:
- Missing PII
- Delayed ingestion
- Inconsistent dispositions between vendors
- This simulates real-world vendor data variability.

#### 🧮 Defining Data Quality
1. Data Quality Dimensions\
Data quality is defined across four weighted dimensions:
- PII Completeness
- Presence of DOB and SSN
- Disposition Accuracy
- Valid and interpretable case outcomes

2. Freshness (Latency)\
Time difference between record date and ingestion

4. Coverage\
Jurisdictional availability

##### Weighted Scoring Model
Data Quality Score =
  35% PII Completeness
+ 30% Disposition Accuracy
+ 20% Freshness
+ 15% Coverage


Weights can be adjusted based on jurisdiction risk, compliance requirements, or downstream product sensitivity.
