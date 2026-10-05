# TaskFlow Software - Asset Inventory and Risk Register

## Overview

This document provides an overview of the key logical assets used by TaskFlow Software's SaaS project-management platform. The purpose of the asset inventory is to identify important systems and understand the security impact if any of them are compromised.

The complete asset data and risk scores are available in `assets.json`.

## CIA Risk Assessment Method

Each asset is assessed using the CIA security model:

- **Confidentiality (C):** How serious would it be if unauthorized users gained access to the asset or its data?
- **Integrity (I):** How serious would it be if the asset or its data was changed without authorization?
- **Availability (A):** How serious would it be if the asset became unavailable?

Each category is scored from 1 to 5:

| Score | Impact |
|------|------|
| 1 | Very Low |
| 2 | Low |
| 3 | Medium |
| 4 | High |
| 5 | Critical |

The overall risk score is calculated using:

**Risk Score = (Confidentiality + Integrity + Availability) / 3**

Risk levels used in this assessment:

- **1.00 - 1.99:** Very Low
- **2.00 - 2.99:** Low
- **3.00 - 3.49:** Medium
- **3.50 - 4.49:** High
- **4.50 - 5.00:** Critical

## Asset Summary

| ID | Asset | C | I | A | Risk Score | Risk Level |
|---|---|---:|---:|---:|---:|---|
| TF-001 | Web Application | 4 | 5 | 5 | 4.67 | Critical |
| TF-002 | REST API | 4 | 5 | 5 | 4.67 | Critical |
| TF-003 | Customer Database | 5 | 5 | 4 | 4.67 | Critical |
| TF-004 | Authentication Service | 5 | 5 | 5 | 5.00 | Critical |
| TF-005 | CI/CD Pipeline | 3 | 5 | 4 | 4.00 | High |
| TF-006 | Source Code Repository | 4 | 5 | 3 | 4.00 | High |
| TF-007 | Logging and Monitoring System | 3 | 4 | 4 | 3.67 | High |

## Key Findings

The Authentication Service has the highest risk score because a compromise could affect user access, account security, and the availability of the platform.

The Customer Database, REST API, and Web Application are also critical because they process or provide access to important customer and application data.

The CI/CD Pipeline, Source Code Repository, and Logging and Monitoring System are rated as high-risk assets because unauthorized changes or loss of access could affect software deployments, application security, and the SOC analyst's ability to detect incidents.

## Conclusion

This asset inventory gives TaskFlow Software a simple view of its most important logical assets and their security impact. The risk ratings can help the SOC analyst prioritize monitoring, detection rules, and incident response activities in the next stages of the project.