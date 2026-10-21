# TaskFlow Software - SOC Deployment Guide

## 1. Overview

This guide documents the demonstration environment used for the TaskFlow Software SOC Incident Response Package.

The project uses Elastic Cloud, Elasticsearch, Kibana, Sigma detection rules, and simulated security events to demonstrate security monitoring and incident response.

This is a test environment, not a production deployment.

## 2. Requirements

- An Elastic Cloud account and an active Security project
- Authorized access to Kibana and Elastic Security
- Git and VS Code
- A browser and internet connection
- Project files from the GitHub repository

Repository:
https://github.com/mubashirkz/taskflow-soc-incident-response

## 3. Access the Existing Demo

Elastic Security:
https://my-security-project-a4fd4d.kb.us-central1.gcp.elastic.cloud/app/security/get_started

SOC Dashboard:
https://my-security-project-a4fd4d.kb.us-central1.gcp.elastic.cloud/app/r/s/DELQe

1. Open the dashboard URL.
2. Sign in with an authorized account.
3. Set the time range to Last 30 days, or select a custom range covering the October 2026 test events.
4. Review the security monitoring charts.

The demo requires appropriate project permissions. Public access has not been verified.

## 4. Set Up an Elastic Cloud Environment

1. Sign in to Elastic Cloud.
2. Create or select an Elastic Security project.
3. Open Kibana.
4. Open the Elasticsearch Dev Tools console.
5. Create an index named taskflow-logs if it does not already exist.
6. Ingest the sample events from logs/taskflow_events.ndjson, adapting the file to the Elasticsearch Bulk API format if necessary.
7. Confirm successful indexing responses.

Example verification query in Kibana Discover:

```esql
FROM taskflow-logs
| LIMIT 100
```

The original demonstration processed 18 sample documents during testing. Results in a fresh deployment may differ.

## 5. Configure Detection Rules

The rules/ directory contains:

- phishing_detection.yml
- phishing_detection.lucene
- web_injection_detection.yml
- web_injection_detection.lucene

To reproduce the Kibana detections:

1. Open Elastic Security.
2. Navigate to Detection Rules.
3. Create a custom query rule using the taskflow-logs index.
4. Configure the phishing detection query:

```kql
event.category:email AND event.action:received AND threat.indicator.type:phishing
```

5. Create a second rule for web injection:

```kql
event.category:web AND event.action:request AND threat.indicator.type:web-injection
```

6. Set the rule severity to High and configure an appropriate execution schedule.
7. Enable both rules.
8. Verify rule execution and test alerts using authorized simulated events.

These are the KQL queries used in the original demonstration. The Sigma YAML and converted Lucene files are provided separately.

## 6. Security Monitoring Dashboard

The dashboard configuration is stored in:

dashboards/taskflow_soc_dashboard.json

The original dashboard includes:

- Security event monitoring
- Severity distribution
- Source IP activity
- Affected application endpoints
- Web Application Asset Activity (TF-001)

The dashboard was configured to refresh every 30 seconds.

To reproduce it, review the supplied JSON and configure or import the compatible dashboard objects in Kibana. The file's compatibility with Kibana Saved Objects import must be verified before attempting a direct import.

Use the October 2026 test-event time range to display the historical data.

Dashboard screenshot:
screenshots/taskflow_soc_dashboard.png

## 7. Incident Response Playbooks

The playbooks/ directory contains Markdown and PDF versions of:

- Phishing incident response
- Ransomware incident response
- API injection incident response

Each playbook describes detection, investigation, containment, eradication, recovery, and incident closure.

Use these documents as reference procedures during authorized investigations.

## 8. Tabletop Exercise

The tabletop/ directory contains:

- mock_alerts.json
- tabletop_exercise_report.md

The exercise simulated an API injection incident affecting the TaskFlow REST API.

The exercise documented investigation decisions and proposed response actions. No live containment or recovery actions were performed.

## 9. Validation Evidence

Review the following project evidence:

- screenshots/elastic_log_index.png
- screenshots/phishing_rule_enabled.png
- screenshots/web_injection_rule_enabled.png
- screenshots/taskflow_soc_dashboard.png
- reports/false_positive_test_results.md
- reports/task3_incident_investigation.md

Ten benign test events produced zero new false-positive alerts during the controlled test. This does not establish production detection accuracy.

## 10. Troubleshooting

### Dashboard charts appear empty

Change the Kibana time filter to Last 30 days or select a custom time range covering the test events.

### Detection rules do not generate alerts

Verify the index name, event field mappings, KQL queries, rule execution schedule, and enabled status.

### Elasticsearch queries return no documents

Check the taskflow-logs index, ingestion results, and timestamp filters.

### Demo URL requests authentication

Sign in using an account with access to the Elastic Cloud project. Do not publish administrator credentials.

### Elastic Cloud trial expires

The live demo may become unavailable. The repository retains the configuration files, reports, screenshots, and playbooks for reference.

## 11. Recommended Next Steps

1. Verify detection rules against additional authorized test cases.
2. Improve API request logging and event correlation.
3. Enable database audit logging.
4. Test WAF blocking and API rate limiting.
5. Conduct authorized recovery and security regression testing.
6. Review and maintain the incident response playbooks.

## 12. Security Notes

All security events used in this project are simulated.

Do not upload credentials, API keys, private customer information, or other secrets to the public repository.

The environment and procedures are intended for authorized security testing and demonstration only.
