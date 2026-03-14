```
# Attack Timeline

## Overview

This timeline reconstructs the intrusion events observed on the Ubuntu server during the SOC lab simulation.

The sequence of events was derived from authentication logs collected from:

/var/log/auth.log

These logs were ingested into Elastic SIEM through Filebeat and analyzed in Kibana.

---

## Timeline of Events

| Time | Event | Log Evidence | Interpretation |
|-----|------|-------------|---------------|
| 20:35:35 | SSH authentication failure | pam_unix(sshd:auth): authentication failure | Attacker begins SSH brute-force attempt |
| 20:35:36 | Additional authentication failures | pam_unix(sshd:auth): authentication failure | Multiple login attempts indicate credential guessing |
| 20:48:11 | Privilege escalation | pam_unix(sudo-i:session): session opened for user root by ragnar | Attacker escalates privileges after gaining access |
| 21:03:05 | Backdoor password modification | pam_unix(passwd:chauthtok): password changed for backdoor | Persistence account created or modified |
| 21:07:33 | Failed backdoor login attempt | authentication failure user=backdoor | Attacker testing persistence account |
| 21:07:49 | Continued authentication failures | connection closed by authenticating user backdoor | Further login attempts |
| 21:07:59 | Successful SSH login using backdoor | session opened for user backdoor(uid=1001) | Persistence account successfully authenticated |
| 21:08:00 | Interactive session created | systemd-logind: New session for user backdoor | Attacker gains interactive access |
| 21:08:00 | Session confirmed | pam_unix(systemd-user:session): session opened | Active attacker session established |

---

## Attack Flow Reconstruction

Reconnaissance  
↓  
SSH brute-force attempts  
↓  
Successful login
↓
Privilege escalation  
↓  
Credential access  
↓  
Persistence creation  
↓  
Backdoor login  
↓  
Active attacker session

---

## Security Significance

This timeline demonstrates a complete intrusion chain including:

- authentication attacks
- privilege escalation
- persistence establishment
- attacker re-entry

The correlation of these events enabled the SOC analyst to identify and investigate the compromise.


## Security Significance

This timeline demonstrates a full attack progression from initial targeting to persistence and re-entry.

It also shows how Elastic SIEM can be used to correlate events and reconstruct the incident for investigation and response.
```
