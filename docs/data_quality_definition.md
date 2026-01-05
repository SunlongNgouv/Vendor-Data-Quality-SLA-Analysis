🧪 SQL: Data Quality Metrics

Assumed business requirements are:

Allowed values and formats
1. record_value: start with A** or B**
2. vendor: value should be in (vendor A, vendor B)
3. county: counties in the US only
4. dob: format should be YYYY/MM/DD
5. ssn: format should be XXX-XX-XXXX for individual
6. disposition: value should be in (Convicted, Dismissed, Pending)
7. record_date and ingest_time: dates should be in TimeStamp

Cross-column logic
1. dates in ingest_time should be later than the dates in 'record_date'.
2. if disposition is not null, record_date should be not null.
3. if disposition is 'pending', record_date should be less than 30 days of ingest_time.
3. convicted records should have ssn.
4. age should be reasonable with under 100 years old.
5. date of birth should be earlier than record_date.
6. ingest_time should be within SLA at 48 hours from record_date.

Cross-row logic
1. record_id should map to one ssn
2. same person should not appear twice in the records