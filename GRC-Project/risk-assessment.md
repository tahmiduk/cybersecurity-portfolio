# GRC Risk Assessment Report

**Organisation:** NexaTech Solutions  
**Report Date:** April 2026  
**Analyst:** Mohammad Ahnaf Tahmid  
**Version:** 1.0  
**Classification:** Confidential  

---

## 1. Executive Summary

NexaTech Solutions is a 50-person UK-based software company 
that processes customer personal data. This report presents 
a full risk assessment conducted in accordance with ISO 27001 
and GDPR requirements.

The assessment identified 5 key risks across the organisation. 
Two risks were rated HIGH, two MEDIUM and one LOW. 
Immediate remediation is recommended for all HIGH rated risks.

---

## 2. Scope

| Item | Detail |
|---|---|
| Organisation | NexaTech Solutions |
| Employees | 50 |
| Location | London, UK |
| Data Processed | Customer personal data |
| Frameworks Applied | ISO 27001, GDPR |
| Assessment Date | April 2026 |

---

## 3. Risk Identification

The following risks were identified through review of 
NexaTech Solutions' operations, systems and data handling 
processes.

| Risk ID | Risk Description | Category |
|---|---|---|
| R-001 | Unauthorised access to customer data | Data Security |
| R-002 | Phishing attack on employees | Human Factor |
| R-003 | Lack of data backup and recovery plan | Business Continuity |
| R-004 | Unpatched software vulnerabilities | Technical |
| R-005 | Non-compliance with GDPR requirements | Compliance |

---

## 4. Risk Analysis

Each risk is scored using the following matrix:

**Likelihood:** 1 (Rare) → 5 (Almost Certain)  
**Impact:** 1 (Negligible) → 5 (Critical)  
**Risk Score = Likelihood × Impact**

| Risk ID | Likelihood | Impact | Risk Score |
|---|---|---|---|
| R-001 | 4 | 5 | 20 |
| R-002 | 5 | 4 | 20 |
| R-003 | 3 | 4 | 12 |
| R-004 | 4 | 4 | 16 |
| R-005 | 3 | 5 | 15 |

---

## 5. Risk Evaluation

| Risk Score | Rating |
|---|---|
| 1 - 6 | 🟢 LOW |
| 7 - 12 | 🟡 MEDIUM |
| 13 - 19 | 🟠 HIGH |
| 20 - 25 | 🔴 CRITICAL |

| Risk ID | Risk Description | Score | Rating |
|---|---|---|---|
| R-001 | Unauthorised access to customer data | 20 | 🔴 CRITICAL |
| R-002 | Phishing attack on employees | 20 | 🔴 CRITICAL |
| R-003 | Lack of data backup and recovery plan | 12 | 🟡 MEDIUM |
| R-004 | Unpatched software vulnerabilities | 16 | 🟠 HIGH |
| R-005 | Non-compliance with GDPR requirements | 15 | 🟠 HIGH |

---

## 6. Risk Treatment

### R-001 — Unauthorised Access to Customer Data 🔴 CRITICAL
**Treatment:** Mitigate  
- Implement Role-Based Access Control (RBAC)
- Enforce Multi-Factor Authentication (MFA)
- Conduct quarterly access reviews
- Encrypt all customer data at rest and in transit

### R-002 — Phishing Attack on Employees 🔴 CRITICAL
**Treatment:** Mitigate  
- Deliver mandatory phishing awareness training
- Implement email filtering and anti-phishing tools
- Conduct simulated phishing exercises quarterly
- Establish clear incident reporting procedures

### R-003 — Lack of Data Backup and Recovery Plan 🟡 MEDIUM
**Treatment:** Mitigate  
- Implement automated daily backups
- Store backups in a secure offsite/cloud location
- Test backup restoration every 3 months
- Document and maintain a Business Continuity Plan (BCP)

### R-004 — Unpatched Software Vulnerabilities 🟠 HIGH
**Treatment:** Mitigate  
- Implement a patch management policy
- Apply critical patches within 48 hours of release
- Conduct monthly vulnerability scans using Nmap
- Maintain an asset inventory of all software versions

### R-005 — Non-Compliance with GDPR Requirements 🟠 HIGH
**Treatment:** Mitigate  
- Appoint a Data Protection Officer (DPO)
- Conduct a full GDPR audit of data processing activities
- Update Privacy Policy and Data Retention Policy
- Train all staff on GDPR obligations annually

---

## 7. Risk Monitoring

| Risk ID | Review Frequency | Owner |
|---|---|---|
| R-001 | Quarterly | IT Security Manager |
| R-002 | Quarterly | HR & IT Security |
| R-003 | Every 3 months | IT Manager |
| R-004 | Monthly | IT Security Team |
| R-005 | Annually | Data Protection Officer |

---

## 8. Conclusion

This risk assessment identified 5 risks across NexaTech 
Solutions' operations. Two risks were rated CRITICAL and 
require immediate attention:

- **R-001** — Unauthorised access to customer data
- **R-002** — Phishing attack on employees

All identified risks have been assigned treatment plans and 
monitoring schedules. It is recommended that NexaTech 
Solutions reviews this risk assessment annually or following 
any significant change to the business.

---

## 9. References

- ISO/IEC 27001:2022 — Information Security Management
- UK GDPR — General Data Protection Regulation
- NCSC Cyber Essentials Framework
- NIST SP 800-30 — Risk Assessment Guide

---

**Report prepared by:** Mohammad Ahnaf Tahmid  
**Date:** April 2026  
**GitHub:** github.com/tahmiduk/cybersecurity-portfolio
