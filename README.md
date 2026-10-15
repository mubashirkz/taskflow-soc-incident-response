# TaskFlow Software SOC Incident Response Package

## Overview

This project focuses on building a practical SOC incident response solution for TaskFlow Software, a SaaS project-management company.

The project covers asset risk assessment, detection engineering, security monitoring, incident response playbooks, and a final hand-over package.

## Project Tasks

1. Asset Inventory and Risk Register
2. Sigma Detection Rules
3. Security Monitoring Dashboard
4. Incident Response Playbooks and Tabletop Exercise
5. Final Hand-over Package

## Task 1 - Asset Inventory and Risk Register

Task 1 identifies the important logical assets used by TaskFlow Software and evaluates their security impact using the CIA triad:

- Confidentiality
- Integrity
- Availability

Each asset is scored from 1 to 5. The overall risk score is calculated by averaging the Confidentiality, Integrity, and Availability scores.

Seven assets were assessed, including the web application, REST API, customer database, authentication service, CI/CD pipeline, source code repository, and logging and monitoring system.

## Files

- [`assets.json`](assets.json) - Contains the asset inventory, CIA scores, and overall risk ratings.
- [`assets.md`](assets.md) - Explains the risk assessment methodology and summarizes the findings.

## Key Finding

The Authentication Service received the highest risk score of **5.0 (Critical)**. The Web Application, REST API, and Customer Database were also identified as critical assets.

These results will help prioritize monitoring and detection rules in the next stages of the project.

## Status

- [x] Task 1 - Asset Inventory and Risk Register
- [x] Task 2 - Sigma Detection Rules
- [ ] Task 3 - Security Monitoring Dashboard
- [ ] Task 4 - Incident Response Playbooks and Tabletop Exercise
- [ ] Task 5 - Final Hand-over Package

## Author

Mubashir Ahmad  
Cyber Security Intern


### Task 2 — Sigma Detection Rules in Elastic Stack

I implemented and tested Sigma detection rules in Elastic Security to identify simulated phishing emails and web-injection attacks. I converted the detection logic into Elasticsearch-compatible queries, configured SIEM rules in Kibana, and verified that both attack scenarios generated security alerts. I also tested the rules against 10 benign log events and observed zero false-positive alerts (0%). The testing was performed using a controlled sample dataset, so the results do not represent production accuracy.


### Elastic Cloud Log Index Evidence

I configured an Elastic Cloud Security Serverless project and ingested sample security events into the `taskflow-logs` index.

I verified the indexed data using Kibana Discover with the following ES|QL query:

```esql
FROM taskflow-logs
| LIMIT 100
```

The query successfully processed 18 documents, including simulated security events and benign test logs.

**Evidence — Elastic log index in Kibana Discover:**

![Elastic Cloud log index showing 18 documents](screenshots/elastic_log_index.png)


### Kibana Detection Rules — Deployment Evidence

I configured two custom detection rules in Elastic Security using the `taskflow-logs` index. Both rules are enabled and have successfully executed.

#### 1. Phishing Email Detection

- Rule: `TaskFlow Suspicious Phishing Email`
- Index: `taskflow-logs`
- Query language: KQL
- Severity: High
- MITRE ATT&CK: T1566
- Status: Enabled

KQL query configured in Kibana:

```kql
event.category:email AND event.action:received AND threat.indicator.type:phishing
```

![Enabled phishing detection rule](screenshots/phishing_rule_enabled.png)

#### 2. Web Injection Detection

- Rule: `TaskFlow Suspicious Web Injection`
- Index: `taskflow-logs`
- Query language: KQL
- Severity: High
- MITRE ATT&CK: T1190
- Status: Enabled

KQL query configured in Kibana:

```kql
event.category:web AND event.action:request AND threat.indicator.type:web-injection
```

![Enabled web injection detection rule](screenshots/web_injection_rule_enabled.png)

### Detection Validation

Both rules previously generated alerts during controlled attack simulations. I also tested 10 benign events and observed zero new false-positive alerts (0/10 = 0%).

These results demonstrate the configured detection workflow on a limited simulated dataset, not production detection accuracy.


### Sigma-to-Elasticsearch Query Conversion

The original Sigma rules and their converted Lucene queries are stored in the `sigma/` directory.

| Detection | Original Sigma rule | Converted Lucene query |
|---|---|---|
| Phishing | [phishing_detection.yml](sigma/phishing_detection.yml) | [phishing_detection.lucene](sigma/phishing_detection.lucene) |
| Web injection | [web_injection_detection.yml](sigma/web_injection_detection.yml) | [web_injection_detection.lucene](sigma/web_injection_detection.lucene) |

**Converted phishing query (Lucene):**

```text
event.category:email AND event.action:received AND threat.indicator.type:phishing
```

**Converted web-injection query (Lucene):**

```text
event.category:web AND event.action:request AND threat.indicator.type:web\-injection
```

The corresponding detection rules are configured and enabled in Kibana using KQL. Screenshots above show their enabled status, index patterns, and deployed queries.


## Task 3 - SOC Security Monitoring Dashboard

Created a security monitoring dashboard using Elastic Stack and Kibana.

### Dashboard Features
- Security event monitoring
- Severity distribution visualization
- Source IP activity analysis
- Automatic refresh every 30 seconds

### Testing Results
- 18 sample log events analyzed
- 5 potential security events identified
- Severity distribution: 80% High, 20% Medium
- Source IP activity visualized using a bar chart

### Dashboard Evidence
![TaskFlow SOC Dashboard](screenshots/taskflow_soc_dashboard.png)

### Tools Used
- Elastic Cloud
- Kibana
- Elasticsearch
- ES|QL
