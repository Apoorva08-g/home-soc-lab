Incident Report 002 — Nmap Reconnaissance Scan Detected

Date: 05/06/2026
Severity: Medium
Status: Resolved

Summary:
Wazuh detected a port scan against ubuntu-victim originating from 192.168.1.12. The scan was identified using a custom detection rule (ID 100002) created to address a detection gap where default Wazuh rules did not flag nmap scans.

Timeline:
June 5, 2026 @ 23:11:26 ubuntu-victim nmap scan detected (Rule 100002, 8)

Evidence:
Source IP: 192.168.1.12
Target IP: 192.168.1.27
Rule ID: 100002 (custom rule)
Total alerts: 403
Detection method: SSH connection closed without identification string (nmap signature behavior)

MITRE ATT&CK
Tactic: Reconnaissance
Technique: T1046 — Network Service Discovery

Custom Rule Created
```xml
<rule id="100002" level="8">
  <if_sid>5722</if_sid>
  <match>Connection closed by</match>
  <description>nmap scan detected from $(data.srcip)</description>
  <group>recon,nmap,</group>
</rule>
```

Conclusion
Default Wazuh ruleset did not detect reconnaissance scans. A custom rule was developed and deployed, successfully closing this detection gap. Recommend adding similar custom rules for other scan types (SYN scan, UDP scan) and reviewing default ruleset 
coverage periodically.
