INCIDENT RESPONSE REPORT 001

Date: 04/06/2026
Severity: High
Status: Resolved

Summary: Wazuh detected multiple ssh authentication failures from an IP Address 192.168.1.12 targeting user: victim on the ubuntu-victim. A total of 7 failed attempts were recorded before wazuh rule 5763 triggered a High severity Brute Force Alert. 

Timeline:
FIRST ATTEMPT: Jun 04 08:07:22 ubuntu-victim sshd-session[4100]: Failed password for victim from 192.168.1.12 port 40068 ssh2
Jun 04 08:07:22 ubuntu-victim sshd-session[4097]: Failed password for victim from 192.168.1.12 port 40034 ssh2
Jun 04 08:07:22 ubuntu-victim sshd-session[4098]: Failed password for victim from 192.168.1.12 port 40038 ssh2
Jun 04 08:07:23 ubuntu-victim sshd-session[4101]: Failed password for victim from 192.168.1.12 port 40066 ssh2
Jun 04 08:07:23 ubuntu-victim sshd-session[4102]: Failed password for victim from 192.168.1.12 port 40088 ssh2
Jun 04 08:07:23 ubuntu-victim sshd-session[4104]: Failed password for victim from 192.168.1.12 port 40098 ssh2
FINAL ATTEMPT: Jun 04 08:07:23 ubuntu-victim sshd-session[4105]: Failed password for victim from 192.168.1.12 port 40106 ssh2
WAZUH ALERT TRIGERRED: Jun 4, 2026 @ 13:37:24.927 ubuntu-victim sshd: brute force trying to get access to the system. Authentication failed.

Note: Raw log timestamps are in UTC+00:00. 
Wazuh dashboard timestamps are in IST (UTC+5:30).
08:07 UTC = 13:37 IST

Evidence:

- Attacker IP: 192.168.1.12
- Target IP: 192.168.1.27
- Target hostname: ubuntu-victim
- Target username: victim
- Rule ID: 5763
- Rule description: sshd: brute force trying to get access to the system
- Login attempts: 8
- Total Wazuh alerts generated: 56
- Rule frequency threshold: 8 attempts

MITRE ATT&CK

- Tactic: Credential Access
- Technique: T1110.001 — Brute Force: Password Guessing

Conclusion:

The brute force attack was unsuccessful as no 
authentication was completed. However the following 
actions are recommended:

1. Change the password for user 'victim' immediately
2. Block source IP 192.168.1.12 at the firewall
3. Review login history to confirm no successful 
   access was gained
4. Scan other systems on the network for similar 
   alerts from the same source IP
5. Consider implementing SSH fail2ban to automatically 
   block IPs after repeated failures
