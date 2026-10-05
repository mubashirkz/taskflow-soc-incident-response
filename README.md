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
- [ ] Task 2 - Sigma Detection Rules
- [ ] Task 3 - Security Monitoring Dashboard
- [ ] Task 4 - Incident Response Playbooks and Tabletop Exercise
- [ ] Task 5 - Final Hand-over Package

## Author

Mubashir Ahmad  
Cyber Security Intern