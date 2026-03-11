# NMAP Scan Report
**Date:** 11/03/2026  
**Analyst:** Tahmid 
**Target Network:** 10.0.2.0/24  

## Hosts Discovered
| IP | Role |
|---|---|
| 10.0.2.2 | Windows Host/Gateway |
| 10.0.2.3 | DNS Server |
| 10.0.2.15 | Kali Linux (Analyst Machine) |

## Critical Findings

### Finding 1 — SMB Port 445 Open 🔴 HIGH RISK
- Port 445 open on 10.0.2.2
- SMB vulnerabilities exploited by WannaCry ransomware
- **Recommendation:** Restrict SMB access, apply latest patches

### Finding 2 — MySQL Port 3306 Exposed 🔴 HIGH RISK
- Database port publicly accessible
- Risk of brute force/unauthorised access
- **Recommendation:** Restrict to localhost only

### Finding 3 — HTTP Services on 5000/5357 🟡 MEDIUM
- Two HTTP services running
- **Recommendation:** Investigate and disable if unnecessary

## Tools Used
- Nmap 7.95
- Kali Linux

## Summary
3 hosts discovered on network 10.0.2.0/24.
2 high risk findings identified requiring immediate attention.
