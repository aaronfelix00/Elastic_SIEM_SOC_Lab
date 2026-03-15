## Overview
This document correlates security events observed across system logs and the Elastic SIEM platform to identify the full attack chain.

By correlating authentication logs, privilege escalation events, and file access activity, the SOC analyst can reconstruct the attack progression.


## Log Source

Primary log monitored:
```
/var/log/auth.log
```
Collected using:

- Filebeat
- Elasticsearch
- Kibana


## Correlated Events

### Stage 1 – Reconnaissance

Indicators:

- External host scanning the server
- Service enumeration

Tool:
```
nmap
```
### Stage 2 – Brute Force Attempts

Observed indicators:

- Multiple failed SSH login attempts
- Rapid authentication failures

Log example
```
Failed password for ragnar from 10.0.0.115
```

Detection rule triggered:
```
SSH Brute Force Detection
```
### Stage 3 - Successful Authentication
Indicators:
```
Accepted password for user
```
This indicates that the attacker successfully authenticated after multiple attempts.


### Stage 4 – Privilege Escalation

Observed indicators:
```
sudo: session opened for user root
```

Detection rule triggered:
```
Privilege Escalation Detection
```

### Stage 5 - Sensitive File Access
Observed activity:
```
cat/etc/shadow
```

This action indicates credential harvesting.

Detection rule triggered:
```
Credential Access Detection
```

## Correlation Summary

| Event | Detection |
|------|------|
| Multiple SSH failures | Brute force attempt |
| Successful login | Account compromise |
| sudo command execution | Privilege escalation |
| Access to ```/etc/shadow``` | Credential dumping |


## Conclusion

Correlating events across authentication logs and SIEM alerts enables SOC analysts to identify the entire attack chain from reconnaissance to credential access.
