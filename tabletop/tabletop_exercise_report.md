# TaskFlow Software – SOC Tabletop Exercise Report

**Exercise ID:** INC-TF-001  
**Exercise Date:** 20 October 2026  
**Scenario:** API Injection Attack  
**Exercise Type:** Simulated Incident Response  
**Severity:** High – Potential Critical Impact  
**Playbook:** IR-PB-003 – API Injection  
**Primary Role:** SOC Analyst  
**Environment:** TaskFlow Software SaaS Beta

## 1. Exercise Objective

The objective of this tabletop exercise is to evaluate TaskFlow Software's ability to detect, investigate, contain, and respond to a simulated API injection attack.

The exercise uses mock security alerts and the API Injection Incident Response Playbook developed during Task 4.

No real systems were attacked, isolated, or modified.

## 2. Affected Assets

| Asset ID | Asset Name | Risk Level |
|---|---|---|
| TF-002 | REST API | Critical |
| TF-003 | Customer Database | Critical |
| TF-001 | Web Application | Critical |
| TF-007 | Logging and Monitoring System | High |

The primary target is TF-002. TF-003 is considered potentially at risk, but database compromise has not been confirmed.

## 3. Simulated Incident Timeline

All times are UTC on 20 October 2026.

| Time | Simulated Event | Severity |
|---|---|---|
| 09:00 | Suspicious GET request to `/api/projects`, HTTP 400 | Medium |
| 09:02 | Repeated suspicious requests from 203.0.113.45, HTTP 403 | High |
| 09:05 | Simulated web injection detection alert triggered | High |
| 09:08 | Potential database exposure flagged for investigation | Critical |

**Source IP:** 203.0.113.45 (reserved documentation address)

**Evidence:** `tabletop/mock_alerts.json`

## 4. Investigation and Response Walkthrough

### Phase 1 – Detection

**Responsible:** SOC Analyst

The mock alert sequence was reviewed to identify suspicious API activity.

**Observations:**
- Multiple suspicious requests originated from the same simulated source IP.
- The targeted endpoint was `/api/projects`.
- The sequence contained HTTP 400 and 403 responses.
- A simulated web injection detection alert was generated.

**Decision:** Classify the activity as suspected API injection and begin investigation.

### Phase 2 – Analysis

**Responsible:** SOC Analyst

The simulated events were correlated using timestamps, source IP, target endpoint, and severity.

**Findings:**
- The REST API (TF-002) was the primary target.
- The Customer Database (TF-003) was identified as potentially at risk.
- The mock alerts did not establish successful injection or unauthorized database access.
- Additional API request details and database audit logs would be required.

**Decision:** Maintain high incident priority and escalate if data compromise is confirmed.

### Phase 3 – Containment

**Responsible:** System Administrator / Application Owner

**Proposed actions:**
1. Review available WAF and API gateway logs.
2. Block verified malicious traffic using approved controls.
3. Apply temporary rate limits or endpoint restrictions if required.
4. Revoke compromised API credentials if identified.
5. Preserve relevant logs before disruptive changes.

**Exercise outcome:** Containment actions were discussed as part of the simulation. No live blocking or system changes were performed.

### Phase 4 – Eradication

**Responsible:** Application Developer / System Administrator

**Proposed actions:**
1. Investigate the affected API endpoint for injection vulnerabilities.
2. Review server-side input validation.
3. Use parameterized queries where database queries are involved.
4. Verify authorization and database permissions.
5. Test and deploy any required security fixes through approved procedures.

**Exercise outcome:** No actual vulnerability was confirmed or remediated.

### Phase 5 – Recovery

**Responsible:** Application Owner / SOC Analyst

**Proposed actions:**
1. Validate the security of affected endpoints.
2. Verify legitimate API functionality.
3. Review database integrity and access records.
4. Restore restricted services after authorization.
5. Monitor for repeated suspicious activity.

**Exercise outcome:** Recovery procedures were reviewed but not executed on live systems.

## 5. Observed Gaps

| Gap ID | Identified Gap | Impact |
|---|---|---|
| GAP-001 | Mock alerts lack full API request details | Difficult to confirm injection attempts |
| GAP-002 | Database audit evidence is unavailable | Cannot verify possible data exposure |
| GAP-003 | Automated containment is not demonstrated | Response may depend on manual intervention |
| GAP-004 | Recovery procedures are not technically tested | Recovery effectiveness remains unverified |

## 6. Improvement Log

| ID | Improvement Action | Owner | Priority |
|---|---|---|---|
| IMP-001 | Improve API request logging and correlate events with Elastic Security | SOC Analyst / Developer | High |
| IMP-002 | Enable and review database audit logging for sensitive operations | Database Administrator | High |
| IMP-003 | Develop and test approved WAF blocking and API rate-limiting procedures | System Administrator | High |
| IMP-004 | Conduct an authorized API recovery and security regression test | Application Developer | Medium |

These actions are recommendations from the tabletop scenario, not completed technical changes.

## 7. Exercise Findings and Lessons Learned

The mock alert sequence demonstrated how suspicious API activity could be identified and correlated using a consistent source IP, endpoint, and timeline.

The exercise highlighted the importance of having sufficient request and database audit evidence before confirming a successful attack.

It also demonstrated the need for clearly assigned responsibilities, approved containment procedures, and tested recovery steps.

## 8. Exercise Conclusion

The tabletop walkthrough covered detection, analysis, proposed containment, eradication, and recovery decisions using TaskFlow's API Injection Playbook.

The mock alerts support a suspected API injection incident, but they do not confirm successful exploitation or customer data exposure.

The identified gaps and improvement actions should be reviewed before considering the response process operationally validated.

**Exercise Status:** Tabletop walkthrough documented; live response testing not performed.

## 9. Supporting Evidence

- `tabletop/mock_alerts.json`
- `playbooks/api_injection_playbook.md`
- `playbooks/api_injection_playbook.pdf`
- `assets.json`
- TaskFlow Elastic Security detection rules and dashboard documentation