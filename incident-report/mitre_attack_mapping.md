## Overview

This document maps the simulated attack activity in the SOC lab to relevant MITRE ATT&CK tactics and techniques.

This helps frame the intrusion using a standardized threat model and demonstrates how the attack aligns with real-world adversary behaviour.

## Mapping Table
| Attack Stage | MITRE ATT&CK Tactic | MITRE ATT&CK Technique |
|-------------|---------------------|-------------------------|
| Reconnaissance | Discovery | T1046 - Network Service Discovery |
| SSH brute force | Credential Access | T1110 - Brute Force |
| Successful SSH login | Initial Access | T1078 - Valid Accounts |
| Privilege escalation using sudo | Privilege Escalation | Elevated execution through abuse of privileged access |
| Credential dumping from ```/etc/shadow``` | Credential Access | T1003 - OS Credential Dumping |
| Backdoor user creation | Persistence | T1136 - Create Account |
| Persistence via account use | Persistence | T1098 - Account Manipulation |
| SSH login using backdoor account | Lateral / Remote Access Context | T1021 - Remote Services |

## Stage-by-Stage Mapping

### 1. Reconnaissance

The attacker first identified exposed services on the target using Nmap.
```
- Tactic: Discovery
- Technique: T1046 - Network Service Discovery
```
### 2. Brute Force Authentication

Hydra was used to attempt multiple username and password combinations against SSH.
```
- Tactic: Credential Access
- Technique: T1110 - Brute Force
```
### 3. Initial Access

The attacker successfully authenticated to the target using valid credentials.
```
- Tactic: Initial Access
- Technique: T1078 - Valid Accounts
```
### 4. Privilege Escalation

The attacker elevated access using ```sudo -i```.
```
- Tactic: Privilege Escalation
- Technique Context: privileged execution using legitimate administrative capabilities
```
### 5. Credential Dumping

After obtaining root privileges, the attacker accessed ```/etc/shadow```.
```
- Tactic: Credential Access
- Technique: T1003 - OS Credential Dumping
```
### 6. Persistence Creation

A new account named backdoor was created on the target system.
```
- Tactic: Persistence
- Technique: T1136 - Create Account
```
### 7. Account Manipulation / Persistence Use

The attacker used the newly created account to re-enter the system.
```
- Tactic: Persistence
- Technique: T1098 - Account Manipulation
```
### 8. Remote Access Through SSH

The backdoor account was used to establish remote access over SSH.
```
- Tactic Context: Remote Services
- Technique: T1021 - Remote Services
```
## Security Relevance

Mapping this lab to MITRE ATT&CK shows that the intrusion is not just a generic lab exercise, but a realistic sequence of adversary actions aligned with widely recognized threat behaviour.

This also helps defenders:

- understand attacker objectives
- organize detections by tactic and technique
- communicate incidents more clearly
- improve threat hunting and rule development

## Summary

The simulated intrusion demonstrated a complete progression across multiple ATT&CK tactics, including:

- Discovery
- Credential Access
- Initial Access
- Privilege Escalation
- Persistence
- Remote Access

