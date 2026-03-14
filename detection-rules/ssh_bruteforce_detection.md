## Overview

SSH brute-force attacks generate a large number of authentication failures within a short time period.

Detecting this pattern allows SOC analysts to identify password guessing attempts against the server.

## Data Source

Linux authentication logs:
```
/var/log/auth.log
```
These logs are collected by Filebeat and ingested into Elasticsearch.

## Detection Logic

The detection looks for multiple failed authentication attempts from the same source IP address.

This shows the  indicator of compromise, log entry and the detection pattern.
![SSH Bruteforce Detection](../screenshots/07_multiple_failed_ssh_authentication_attempts.png)

Typical brute-force pattern:
Multiple failed login attempts
↓
Repeated attempts from same IP
↓
Possible credential guessing attack

## SOC Action

When this pattern is detected, the SOC analyst should:

- identify the source IP address
- determine the targeted usernames
- check whether a successful login followed the failures

