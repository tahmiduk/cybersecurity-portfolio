# Oski Lab — CyberDefenders Writeup

**Platform:** CyberDefenders  
**Category:** Threat Intel  
**Difficulty:** Easy  
**Date:** May 2026  
**Analyst:** Mohammad Ahnaf Tahmid  
**Score:** 7/7 — 100% Completed  

---

## Scenario
An accountant received an email titled "Urgent New Order" 
containing a malicious PPT file. The SIEM flagged a 
potentially malicious file download. My task was to analyse 
the malware using sandbox and threat intelligence tools.

---

## Tools Used
- VirusTotal
- ANY.RUN Sandbox
- MITRE ATT&CK Framework

---

## Investigation

### Q1 — Malware Creation Time
**Answer: 2023-09-28 17:40**

Found by looking up the file hash on VirusTotal and 
checking the Details tab for the compilation timestamp.

### Q2 — C2 Server
**Answer: http://171.22.28.221/5c06c05b7b34e8e6.php**

Found in VirusTotal under Relations → Contacted URLs. 
The malware communicates with this IP address to receive 
commands from the attacker.

### Q3 — First Library Requested
**Answer: sqlite3.dll**

Found in ANY.RUN sandbox report under loaded modules. 
Stealc malware loads sqlite3.dll to access browser 
databases and steal saved passwords and cookies.

### Q4 — RC4 Decryption Key
**Answer: 5329514621441247975720749009**

Found in ANY.RUN config extractor. The malware uses 
this RC4 key to decrypt its own configuration, hiding 
the C2 server address from antivirus detection.

### Q5 — MITRE ATT&CK Technique
**Answer: T1555**

T1555 — Credentials from Password Stores. The malware 
uses this technique to steal saved passwords from 
browsers like Chrome and Firefox by reading their 
local SQLite databases.

### Q6 — DLL Deletion Directory
**Answer: C:\ProgramData**

Found in ANY.RUN behaviour activities. The malware 
runs this command to delete all DLL files:
del "C:\ProgramData\*.dll"
This is anti-forensics — covering its tracks after 
data exfiltration.

### Q7 — Self-Delete Timer
**Answer: 5 seconds**

Found in the same CMD command:
timeout /t 5
The malware waits 5 seconds before deleting itself 
and all associated DLL files.

---

## Attack Timeline

| Step | Action |
|---|---|
| 1 | Victim receives phishing email with malicious PPT |
| 2 | PPT downloads and executes Stealc malware |
| 3 | Malware loads sqlite3.dll to access browser databases |
| 4 | Credentials stolen and sent to C2 server |
| 5 | Malware deletes DLLs from C:\ProgramData |
| 6 | Malware self-deletes after 5 seconds |

---

## Key Learnings
- Stealc is a credential stealer targeting browser passwords
- SQLite databases store browser credentials locally
- RC4 encryption is used to hide malware configuration
- Anti-forensics techniques delete evidence after exfiltration
- MITRE ATT&CK T1555 covers credential theft from browsers
- Always check VirusTotal Relations tab for C2 servers

## Recommendations
- Block execution of files from Temp directories
- Monitor outbound connections to unknown IPs
- Enable browser credential protection
- Implement email filtering for malicious attachments
- Deploy EDR solution to detect suspicious DLL loads

---

**GitHub:** github.com/tahmiduk/cybersecurity-portfolio
