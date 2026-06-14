INCIDENT REPORT 003

Date: 11/06/2026
Severity: High
Status: Resolved

Summary: Wazuh detected a privilege escalation attack on ubuntu-victim. After gaining initial SSH access as user 'victim' from 192.168.1.12, the attacker exploited a sudo misconfiguration (NOPASSWD on /usr/bin/find) to 
spawn a root shell, achieving full system compromise.

Timeline:
Jun 11, 2026 @ 23:07:59.933 ubuntu-victim Successful sudo to ROOT executed. 3 5402
Jun 11, 2026 @ 23:07:11.921 ubuntu-victim sshd: authentication success.

Evidence:
- Attacker IP: 192.168.1.12
- Target IP: 192.168.1.27
- Target hostname: ubuntu-victim
- Target username: victim
- Rule ID: 5402 
- Rule Description: Successful sudo to ROOT executed.

MITRE ATT&CK
- Tactic: Privilege Escalation, Defense Evasion
- Technique: T1548.003 — Sudo and Sudo Caching

Conclusion:
This represents a critical security breach, the attacker gained full root access. Recommended actions:

1. Remove the NOPASSWD sudo permission for /usr/bin/find
2. Audit sudoers file for other misconfigurations
3. Rotate all credentials on this system
4. Review what actions were taken while root access 
   was held (check bash history, modified files)
5. Block source IP 192.168.1.12
6. Treat this system as compromised — consider 
   rebuilding from a clean image
