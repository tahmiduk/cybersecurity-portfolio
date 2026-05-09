# WebStrike Lab — CyberDefenders Writeup

**Platform:** CyberDefenders  
**Category:** Network Forensics  
**Difficulty:** Easy  
**Date:** May 2026  
**Analyst:** Mohammad Ahnaf Tahmid  
**Score:** 6/6 — 100% Completed  

---

## Scenario
A suspicious file was identified on a company web server. 
The network team captured traffic and prepared a PCAP file 
for review. My task was to analyse the PCAP file to uncover 
how the file appeared and determine the extent of any 
unauthorised activity.

---

## Tools Used
- Wireshark
- IP Geolocation (iplocation.net)

---

## Investigation

### Q1 — Attacker's City
**Answer: Tianjin**

Identified the attacker's IP as 117.11.88.124 by filtering 
HTTP traffic in Wireshark. Looked up the IP using iplocation.net 
which revealed the attack originated from Tianjin, China.

### Q2 — Attacker's User-Agent
**Answer: Mozilla/5.0 (X11; Linux x86_64; rv:109.0) Gecko/20100101 Firefox/115.0**

Expanded the HTTP headers of the attacker's GET request in 
Wireshark. The User-Agent revealed the attacker was using 
Firefox on a Linux machine — likely Kali Linux.

### Q3 — Malicious Web Shell
**Answer: image.jpg.php**

Filtered for POST requests and found the attacker uploaded 
a file named image.jpg.php disguised as an image. The actual 
Content-Type was application/x-php confirming it was a 
web shell. PHP code was visible in the packet data.

### Q4 — Upload Directory
**Answer: /reviews/uploads/**

After uploading the web shell the attacker navigated to 
/reviews/uploads/image.jpg.php to execute it. This confirmed 
the upload directory used by the web server.

### Q5 — Reverse Shell Port
**Answer: 8080**

Filtered for non-HTTP traffic from the web server. Found 
outbound TCP connections from 24.49.63.79 to 117.11.88.124 
on port 8080 — confirming a reverse shell was established 
after the web shell was executed.

### Q6 — Exfiltrated File
**Answer: passwd**

Found a POST request from the web server back to the attacker 
containing Form data with Key: /etc/passwd — confirming the 
attacker used the web shell to steal the Linux password file.

---

## Attack Timeline

| Step | Action |
|---|---|
| 1 | Attacker reconnaissance — browsing the website |
| 2 | Discovered file upload form at /reviews/upload.php |
| 3 | Uploaded web shell disguised as image.jpg.php |
| 4 | Navigated to /reviews/uploads/ to execute web shell |
| 5 | Established reverse shell on port 8080 |
| 6 | Exfiltrated /etc/passwd via POST request |

---

## Key Learnings
- File upload vulnerabilities allow attackers to deploy web shells
- Disguising .php files as images is a common bypass technique
- Reverse shells use outbound connections to evade firewalls
- /etc/passwd contains sensitive user account information
- Always monitor outbound traffic not just inbound

## Recommendations
- Validate file types server side not just client side
- Restrict executable permissions in upload directories
- Monitor outbound connections for unusual ports
- Implement Web Application Firewall (WAF)
- Alert on /etc/passwd access attempts

---

**GitHub:** github.com/tahmiduk/cybersecurity-portfolio
