# TaskFlow SOC Incident Response
## Task 2 — Sigma Detection Accuracy and False-Positive Testing

**Test Date:** October 10, 2026  
**Platform:** Elastic Cloud Security (SIEM)  
**Log Index:** `taskflow-logs`  
**Detection Framework:** Sigma / pySigma Elasticsearch Backend

### 1. Objective

Evaluate whether the two Sigma-derived detection rules identify simulated malicious activity without incorrectly generating alerts for normal business activity.

### 2. Detection Rules Tested

**Rule 1: TaskFlow Suspicious Phishing Email**
- Detects email events labeled as phishing.
- Severity: High
- Risk Score: 73
- MITRE ATT&CK: T1566 — Phishing

**Rule 2: TaskFlow Suspicious Web Injection**
- Detects simulated web-injection activity.
- Severity: High
- Risk Score: 73

### 3. Positive Detection Testing

Two simulated attack scenarios were tested previously:

| Attack Scenario | Detection Result |
|---|---|
| Phishing email | Alert successfully generated |
| Web-injection attempt | Alert successfully generated |

Both alerts were observed in Elastic Security's detection interface.

### 4. False-Positive Testing

Ten benign security events were uploaded to Elasticsearch using the Bulk API.

The dataset contained:
- 5 legitimate email events, including meeting reminders and project updates.
- 5 legitimate web requests, including dashboard and profile access.

The events were identified by the `FPTEST-` message prefix.

An Elasticsearch count query confirmed that all 10 events were successfully indexed.

After checking the enabled detection rules, no new alerts were displayed for the benign test events.

| Detection Rule | Benign Events | Observed False Alerts |
|---|---:|---:|
| Phishing detection | 5 | 0 |
| Web-injection detection | 5 | 0 |
| **Total** | **10** | **0** |

### 5. False-Positive Rate

False-Positive Rate = (False Alerts / Total Benign Events) × 100

**FPR = (0 / 10) × 100 = 0%**

**Result:** The observed false-positive rate was 0%, below the project's required 5% threshold.

### 6. Limitations

- The dataset contained only 10 benign events and two previously successful attack simulations.
- The test used controlled, synthetic events rather than production traffic.
- Detection rules were evaluated using the event fields and labels present in the simulated logs.
- The phishing rule relies on an existing phishing classification label; it does not independently establish that an email is malicious.
- A larger and more varied dataset is needed to assess real-world accuracy.
- The result represents the observed behavior during this test, not a guaranteed production false-positive rate.

### 7. Conclusion

Both Sigma-derived rules successfully generated alerts for their respective simulated attack scenarios. During the subsequent benign-event test, no false-positive alerts were observed.

The testing demonstrated basic detection functionality, successful Elasticsearch log ingestion, and an observed false-positive rate below the required threshold within the controlled lab environment.

