## Overview

The SOC analyst investigates authentication logs to determine whether the brute-force attack resulted in a successful login.

Authentication activity on Ubuntu systems is recorded in:
```
/var/log/auth.log
```
These logs are collected by Filebeat and ingested into Elastic SIEM.

## Failed Authentication Attempts

The analyst observes repeated login failures.

## Evidence
![Authentication Failure Logs](../screenshots/07_multiple_failed_ssh_authentication_attempts.png)
![Authention Failures in SIEM](../screenshots/07b_multiple_failed_login_events_in_kibana_discover.png)

These events indicate that an attacker is attempting to guess credentials.

## Successful Login Event

Eventually a successful authentication event appears.

## Evidence
![Authentication Success](../screenshots/08_successful_ssh_authentication_event.png)

This confirms that the attacker successfully authenticated to the system.

## Security Interpretation

The pattern observed is:
```
multiple failures -> successful login
```

This strongly indicates a successful brute-force compromise.

## Investigation Focus

At this stage the SOC analyst must determine:

- what actions were performed after login
- whether privilege escalation occurred
- whether persistence was established

