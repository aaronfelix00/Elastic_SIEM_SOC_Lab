```
## Overview

A successful authentication event occurring after multiple failed login attempts may indicate that a brute-force attack has succeeded.

SOC analysts must identify these events quickly to determine whether the system has been compromised.

## Data Source

Authentication logs collected from:
```
/var/log/auth.log
```

## Detection Indicator

Successful authentication events appear as:
![Successful Authentication](../screenshots/08_successful_ssh_authentication_event.png)

## Detection Logic
Relevant fields:
```
event.category: authentication
event.outcome: success
```
![Successful Authentication on SIEM](../screenshots/09_successful_login_event_in_kibana_discover.png)

## Investigation Focus

SOC analysts should verify:

- the source IP address
- the username used
- whether multiple failures occurred beforehand
- what commands were executed after login

## Security Significance

A successful login after repeated failures strongly indicates that a brute-force attack has succeeded.
```
