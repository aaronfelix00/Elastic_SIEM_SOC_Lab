## Overview
This document reconstructs the sequence of events during the simulated attack based on log analysis and SIEM alerts.

## Attack Timeline

### 1. Reconnaissance

The attacker scanned the target system to identify open services.

Tool used:
```
nmap -sV 10.0.0.99
```
Result:

- SSH service detected on port 22


### 2. SSH Brute Force

The attacker initiated multiple login attempts using Hydra.

Indicators:
```
Failed password for ragnar from 10.0.0.99
```
SIEM Detection:
```
SSH Brute Dorce Detection Rule Triggered
```
### 3. Successful Login

After multiple attempts, the attacker successfully authenticated.

SIEM Detection:
```
Successful SSH Login Rule Triggered
```

Impact:

- Unauthorized access to the server


### 4. Privilege Escalation

The attacker attempted to elevate privileges.

Observed event:
```
sudo command execution
```
SIEM Detection:
```
Sudo Privilege Escalation Rule Triggered
```
![SSH detection alert](../screenshots/18_ssh_bruteforce_detection_alert_in_kibana.png)

### 5. Credential Dumping

The attacker attempted to access sensitive credential storage.

Target file:
```
/etc/shadow
```

### 6. SOC Detection

Elastic SIEM generated alerts indicating suspicious activity.

Alerts triggered:

- SSH brute force
- Privilege escalation
- Sensitive file access


### 7. Incident Response

SOC analyst actions:

- Investigated suspicious login
- Identified attacker IP
- Disabled compromised account
- Detection and removal of backdoor account
- Implemented system hardening (Fail2ban installed and implemented, firewall activation, SSH security)

![Incident Response](../screenshots/22_backdoor_termination_removal_and_validation.png)
![Fail2ban](../screenshots/23_fail2ban_status_verification.png)
![Firewall](../screenshots/24_firewall_security_rules_enabled.png)

## Final Attack Chain
Reconnaissance
↓
SSH Brute Force
↓
Successful Login
↓
Privilege Escalation
↓
Credential Dumping
↓
SOC Detection
↓
Incident Response

## Conclusion

The timeline reconstruction confirms a full attack chain starting from reconnaissance and ending with credential access attempts, which were successfully detected by the Elastic SIEM platform.
