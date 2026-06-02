# Yellow RAT Lab — CyberDefenders Writeup

**Platform:** CyberDefenders  
**Category:** Threat Intel  
**Difficulty:** Easy  
**Date:** June 2026  
**Analyst:** Mohammad Ahnaf Tahmid  
**Score:** 6/6 — 100% Completed  

---

## Scenario
During a regular IT security check at GlobalTech Industries 
abnormal network traffic was detected from multiple 
workstations. Employees' search queries were being redirected 
to unfamiliar websites. My task was to investigate the 
incident using threat intelligence platforms.

---

## Tools Used
- VirusTotal
- Red Canary Threat Intelligence

---

## Investigation

### Q1 — Malware Family Name
**Answer: Yellow Cockatoo RAT**

Found by searching the hash on VirusTotal and navigating 
to Relations → Graph Summary → PEDLL icon → Tree view. 
The malware family Yellow Cockatoo RAT was clearly linked 
in the visualization. Red Canary first documented this 
malware family and their blog provides detailed analysis.

### Q2 — Common Filename
**Answer: 111bc461-1ca8-43c6-97ed-911e0e69fdf8.dll**

Found in VirusTotal under the Details tab → Names section. 
This filename is an IOC that can be used to scan other 
workstations for potential infection using EDR tools or 
antivirus software.

### Q3 — Compilation Timestamp
**Answer: 2020-09-24 18:28**

Found in VirusTotal under the Details tab → Compilation 
Timestamp. The malware was compiled in September 2020 
indicating it is not a new threat and may have active 
variants still in the wild.

### Q4 — First Submitted to VirusTotal
**Answer: 2020-10-15 02:47**

Found in VirusTotal under the Details tab → History section. 
The gap between compilation (September 2020) and first 
submission (October 2020) suggests the malware was active 
in the environment for approximately 3 weeks before detection.

### Q5 — .dat File in AppData
**Answer: solarmarker.dat**

Found in VirusTotal under the Behavior tab → Files Dropped 
section. The malware drops solarmarker.dat in the AppData 
folder as part of its persistence mechanism. This filename 
is also an IOC for scanning infected systems.

### Q6 — C2 Server
**Answer: https://geogold.com**

Found in VirusTotal under the Relations tab → Contacted URLs. 
The malware communicates with geogold.com to receive commands 
from the attacker. This URL should be blocked at the firewall 
and proxy level to prevent further data exfiltration.

---

## Attack Timeline

| Step | Action |
|---|---|
| 1 | Malware compiled September 2020 |
| 2 | Deployed to GlobalTech workstations |
| 3 | Employees' search queries redirected |
| 4 | Malware drops solarmarker.dat in AppData |
| 5 | Establishes connection to C2 server geogold.com |
| 6 | Attacker maintains remote access via RAT |

---

## Key Learnings
- Yellow Cockatoo RAT uses SEO poisoning to spread
- Malware can be active weeks before detection
- .dat files in AppData are common persistence locations
- VirusTotal Relations tab reveals C2 infrastructure
- Compilation timestamps help understand malware age
- Red Canary threat intelligence blog is valuable resource

## Recommendations
- Block geogold.com at firewall and web proxy
- Scan all workstations for solarmarker.dat
- Search for DLL filename as IOC across environment
- Implement DNS filtering to block malicious redirects
- Enable endpoint detection and response (EDR) solution
- Monitor AppData folders for unexpected file creation

---

**GitHub:** github.com/tahmiduk/cybersecurity-portfolio
