# Definition
	- AKA data extrusion, exportation, or theft. Refers to unauthorised transfer of data from computer or other device.
	- Often difficult to detect, as transfer or moving of data within or outside a network can closely resemble typical network traffic.
	- **Advanced Persistent Threats (APTs)**
		- Complex and well-orchestrated cyberattacks targeting high-value organizations or governments. Unlike opportunistic attacks, APTs involve sophisticated and highly-resourced adversaries (often state-sponsored groups) who aim to remain undetected within a target's network for long periods.
- # Detection
	- **Network Monitoring** - Analyze traffic patterns for unusual data transfers,
	  unknown connections, and suspicious activity outside regular hours.
	- **Data Loss Prevention (DLP)** - Detect unauthorized movement of sensitive
	  data within your network or at storage locations.
	- **User Behavior Analytics (UEBA)** - Identify deviations from normal user
	  behavior that could indicate compromised accounts or insider threats.
	- **File Integrity Monitoring** - Detect unexpected changes to critical files,
	  which could signal exfiltration attempts.
	- **Honeypots/Honeytokens** - Trap attackers with fake data or credentials to
	  expose malicious interest.
- # Protection
	- **Strong Access Controls** - Enforce strict authentication (multi-factor
	  where possible) and least privilege principles to limit data access.
	- **Network Segmentation** - Isolate network segments to restrict lateral
	  movement and reduce exfiltration impact.
	- **Encryption** - Protect data at rest and in transit, rendering it useless if
	  stolen.
	- **Vulnerability Management** - Apply security patches promptly to prevent
	  exploit-based intrusion.
	- **Security Training** - Educate employees to spot phishing and social
	  engineering attacks that often lead to exfiltration.