```
# Attack Chain

This document summarizes the full simulated intrusion workflow.

## Attack Stages

1. Reconnaissance using Nmap
2. SSH brute force using Hydra
3. Successful SSH login
4. Privilege escalation using sudo
5. Credential dumping via /etc/shadow
6. Persistence via backdoor account creation
7. Backdoor re-entry
8. SOC detection and response

## Attack Flow

```text
Recon → Brute Force → Initial Access → Privilege Escalation → Credential Access → Persistence → Re-entry → Response
```
```
