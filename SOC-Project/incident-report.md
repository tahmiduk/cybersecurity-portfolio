# Security Incident Report

**Report ID:** IR-2026-001
**Date:** 12/03/2026
**Analyst:** Mohammad Ahnaf Tahmid
**Severity:** HIGH
**Status:** Closed

---

## Executive Summary
A network security assessment was conducted on the internal
network 10.0.2.0/24 using Nmap and Wireshark. The assessment
identified two high severity vulnerabilities and one medium
severity finding on the network gateway (10.0.2.2). Immediate
remediation is recommended.

---

## Scope
| Item | Detail |
|---|---|
| Network | 10.0.2.0/24 |
| Hosts Scanned | 256 |
| Hosts Discovered | 3 |
| Tools Used | Nmap 7.95, Wireshark 4.4.4, Kali Linux |
| Date of Assessment | 12/03/2026 |

---

## Findings Summary
| ID | Severity | Finding |
|---|---|---|
| F-001 | 🔴 HIGH | SMB Port 445 Open |
| F-002 | 🔴 HIGH | MySQL Port 3306 Exposed |
| F-003 | 🟡 MEDIUM | HTTP Services on 5000/5357 |

---

## Detailed Findings

### F-001 — SMB Port 445 Open (HIGH)
**Host:** 10.0.2.2
**Port:** 445/tcp
**Service:** Microsoft-DS (SMB)

**Description:**
Port 445 is open on the network gateway. SMB (Server Message
Block) is the protocol exploited by the WannaCry ransomware
attack in 2017, which affected over 200,000 systems globally.
An exposed SMB port represents a critical attack vector for
ransomware, lateral movement and data exfiltration.

**Risk:**
An attacker on the network could exploit unpatched SMB
vulnerabilities to gain unauthorised access, execute
ransomware or move laterally across the network.

**Recommendation:**
- Restrict SMB access to authorised hosts only via firewall rules
- Apply latest Windows security patches immediately
- Disable SMBv1 if still enabled
- Monitor port 445 traffic for anomalies

---

### F-002 — MySQL Port 3306 Exposed (HIGH)
**Host:** 10.0.2.2
**Port:** 3306/tcp
**Service:** MySQL 8.0.40

**Description:**
A MySQL database server is publicly accessible on port 3306.
Database ports should never be exposed to the network — they
should only accept connections from localhost or trusted
internal IPs. An exposed database port is a critical risk
as it allows direct brute force attacks against the database.

**Risk:**
An attacker could attempt brute force login to gain access
to sensitive data stored in the database, or exploit MySQL
vulnerabilities to achieve remote code execution.

**Recommendation:**
- Restrict MySQL to localhost only (bind-address = 127.0.0.1)
- Implement strong database passwords
- Enable MySQL audit logging
- Consider moving database behind a firewall rule

---

### F-003 — HTTP Services on Ports 5000/5357 (MEDIUM)
**Host:** 10.0.2.2
**Ports:** 5000/tcp, 5357/tcp
**Service:** Microsoft HTTPAPI 2.0

**Description:**
Two HTTP services were identified running on non-standard
ports. Port 5357 is associated with Windows Network
Discovery (WSDAPI). Port 5000 may indicate an application
or service running on the host. Unnecessary services
increase the attack surface of the host.

**Risk:**
Exposed HTTP services could be vulnerable to web-based
attacks. Unnecessary services should be disabled to reduce
attack surface.

**Recommendation:**
- Identify and document what is running on port 5000
- Disable Windows Network Discovery if not required
- Implement web application firewall if services are needed

---

## Traffic Analysis Summary

### DNS Traffic
- Normal DNS resolution observed between 10.0.2.15 and 10.0.2.3
- google.com successfully resolved to 142.250.151.102
- No suspicious DNS queries detected
- No signs of DNS tunnelling or data exfiltration via DNS

### ICMP Traffic
- Successful ping responses from Google (142.250.151.102)
- All requests received replies — healthy outbound connectivity
- TTL values within expected range
- No ICMP flood detected

---

## Risk Matrix
| Finding | Likelihood | Impact | Risk Level |
|---|---|---|---|
| F-001 SMB 445 | High | Critical | 🔴 HIGH |
| F-002 MySQL 3306 | High | Critical | 🔴 HIGH |
| F-003 HTTP 5000/5357 | Medium | Medium | 🟡 MEDIUM |

---

## Recommendations Summary
1. Immediately restrict SMB port 445 via firewall rules
2. Bind MySQL to localhost only
3. Investigate and disable unnecessary HTTP services
4. Apply all pending Windows security patches
5. Conduct regular network scans to monitor for new exposures

---

## Conclusion
The network assessment identified two high severity findings
that require immediate attention. The exposed SMB and MySQL
ports represent significant risk to the organisation. All
recommendations should be implemented as a priority.

**Report prepared by:** Mohammad Ahnaf Tahmid
**Date:** 12/03/2026
**GitHub:** github.com/tahmiduk/cybersecurity-portfolio
