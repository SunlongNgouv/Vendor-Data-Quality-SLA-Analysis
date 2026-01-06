## Finding:
Following a side-by-side data bake-off between Vendor A and Vendor B, the analysis revealed clear trade-offs across data quality dimensions, particularly between accuracy/completeness and freshness.

Vendor A
- Demonstrates higher PII completeness and disposition accuracy, with fewer missing, invalid, or inconsistent values.

- However, the data shows lower freshness, with an average ingestion latency of 30.4 hours, exceeding the target SLA window.

Vendor B

- Delivers consistently fresh data, meeting freshness expectations across all evaluated records.

- This comes with increased data quality risk, as approximately 50% of records are missing key PII fields (DOB and SSN), resulting in lower overall completeness and accuracy.

**Summary:**
Vendor A provides more reliable and accurate records but at the cost of timeliness, while Vendor B offers faster data availability with higher risk related to incomplete PII and potential downstream inaccuracies. The optimal choice depends on whether the priority is data accuracy and compliance or turnaround time and freshness, particularly at the jurisdiction level.

In addition, please refer to 'SLA_breach_report.csv' in 'output' folder for detailed list of high-latency records, including affected vendor, impacted jurisdictions, and responsible personnel's contact email for follow-up and remedies. 

---
## Outcome:

Total vendors and records:
- vendor A = 10
- vendor B = 10

Missing values in vendor A/B:
- county = 0/0
- dob = 0/5
- ssn = 3/5
- disposition = 0/1

Average data ingested latency:
- vendor A = 30.4 hours
- vendor B = 0.5 hour


**Objectives and results:**

Allowed values and formats:
Due to the missing values, the data shows:

1. record_value: start with A** or B**
> pass

2. vendor: value should be in (vendor A, vendor B)
> pass 

3. county: counties in the US only
> pass 

4. dob: format should be YYYY/MM/DD
> fail (5 out of 20 records)

5. ssn: format should be XXX-XX-XXXX for individual
> fail (8 out of 20 records)

6. disposition: value should be in (Convicted, Dismissed, Pending)
> fail (2 out of 20 records)

7. record_date and ingest_time: dates should be in TimeStamp
> pass

Cross-column logic
1. dates in ingest_time should be later than the dates in record_date.
> pass

2. if disposition is not null, record_date should be not null.
> fail (1 out of 20 records)

3. if disposition is 'pending', record_date should be less than 30 days of ingest_time.
> pass

3. convicted records should have ssn.
> fail (2 out of 20 records)

4. age should be reasonable with under 100 years old.
> fail (5 out of 20 records)

5. date of birth should be earlier than record_date.
> fail (5 out of 20 records)

6. ingest_time should be within SLA at 48 hours from record_date.
> pass

Cross-row logic (same key, different values)
1. record_id should map to one ssn
> fail (18 out of 20 records)

2. same person should not appear twice in the records
> pass


Assumed the data quality dimensions by categories are:
> 35% PII Completeness +
> 30% Disposition Accuracy +
> 20% Freshness +
> 15% Coverage

Data Quality Scoring for Vendor A/B:\
**total score = 59.75% / 64.5%**
- PII Completeness = 29.75% / 17.5%
- Disposition Accuracy = 30% / 27%
- Freshness = 0% / 20%
- Coverage = 0% / 0% -- since there is no Jurisdiction coverage in this scenario

SLA ingestion (< 24 hours)
- within SLA = vendor B 100%
- out of SLA = vendor A 100%

Out of SLA records are:

vendor  | record_id | latency_hour |
|-------|--------|--------------|
VendorA | A001   | 26 |            
VendorA | A002   | 26 |
VendorA | A003   | 28 |
VendorA | A004   | 25 |
VendorA | A005   | 50 | 
VendorA | A006   | 49 |
VendorA | A007   | 25 |
VendorA | A008   | 25 |
VendorA | A009   | 25 |
VendorA | A010   | 25 |
