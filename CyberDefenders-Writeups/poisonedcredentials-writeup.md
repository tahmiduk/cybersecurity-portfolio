# PoisonedCredentials Lab — CyberDefenders Writeup

**Platform:** CyberDefenders  
**Category:** Network Forensics  
**Difficulty:** Easy  
**Date:** May 2026  
**Analyst:** Mohammad Ahnaf Tahmid  
**Score:** 5/5 — 100% Completed  

---

## Scenario
The security team detected suspicious network activity 
suggesting LLMNR and NBT-NS poisoning attacks within the 
network. My task was to investigate the network logs and 
examine captured traffic to identify the rogue machine, 
compromised accounts and affected systems.

---

## Tools Used
- Wireshark
- NBNS Filter
- NTLMSSP Filter

---

## What is LLMNR/NBT-NS Poisoning?
When a Windows machine cannot find a hostname it broadcasts 
a query to the whole network. An attacker on the same network 
responds pretending to be the legitimate host. The victim 
machine then sends its credentials to the attacker who 
captures the username and password hash.

This is one of the most common attacks in real corporate 
networks and is directly relevant to SOC analyst roles.

---

## Investigation

### Q1 — Mistyped Query
**Filter used:** `llmnr`  
**Answer: FILESHAARE**

Found by filtering LLMNR traffic and looking for broadcast 
queries from 192.168.232.162. The machine mistyped FILESHARE 
as FILESHAARE — triggering an LLMNR broadcast that the 
attacker exploited.

### Q2 — Rogue Machine IP
**Filter used:** `llmnr`  
**Answer: 192.168.232.215**

Identified by looking for Standard Query Response packets 
in the LLMNR traffic. The rogue machine responded to the 
broadcast query pretending to be the legitimate host.

### Q3 — Second Victim IP
**Filter used:** `llmnr`  
**Answer: 192.168.232.176**

Found by examining the destination IPs of poisoned responses 
from the rogue machine. Two machines received poisoned 
responses — 192.168.232.162 and 192.168.232.176.

### Q4 — Compromised Username
**Filter used:** `ntlmssp`  
**Answer: janesmith**

Found in NTLMSSP authentication packets. After poisoning 
the response the victim machine sent its credentials to 
the rogue machine via NTLM authentication. The username 
janesmith was visible in plain text in the packet data.

### Q5 — Accessed Hostname
**Filter used:** `ntlmssp.challenge.target_info`  
**Answer: ACCOUNTINGPC**

Found by examining the NTLMSSP challenge Target Info field. 
The NetBIOS Computer Name revealed the attacker accessed 
ACCOUNTINGPC after stealing janesmith's credentials via SMB.

---

## Attack Timeline

| Step | Action |
|---|---|
| 1 | 192.168.232.162 mistypes FILESHARE as FILESHAARE |
| 2 | Machine broadcasts LLMNR query to find FILESHAARE |
| 3 | Rogue machine 192.168.232.215 responds to the query |
| 4 | Victim sends NTLM credentials to rogue machine |
| 5 | Attacker captures janesmith's credentials |
| 6 | Attacker uses credentials to access ACCOUNTINGPC via SMB |

---

## Key Learnings
- LLMNR/NBT-NS poisoning exploits Windows name resolution
- Mistyped hostnames trigger broadcast queries attackers exploit
- NTLM credentials are sent automatically to responding hosts
- Usernames are visible in plain text in NTLMSSP packets
- SMB access with stolen credentials = full machine compromise

## Recommendations
- Disable LLMNR and NBT-NS on all Windows machines
- Implement network segmentation
- Enable SMB signing to prevent relay attacks
- Monitor for multiple NTLM authentication failures
- Use Privileged Access Workstations (PAW) for sensitive accounts

---

**GitHub:** github.com/tahmiduk/cybersecurity-portfolio
