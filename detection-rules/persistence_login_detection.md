## Overview

After establishing persistence, attackers may reconnect to the system using a newly created account.

This allows them to regain access even if the original compromised account is disabled.

## Command
```
ssh backdoor@10.0.0.99
```
![Successful backdoor login](../screenshots/16_backdoor_ssh_login_persistence_access.png)

This indicates that the backdoor account successfully authenticated.

## Detection Pattern

Typical persistence behaviour:
```
Account creation
↓
Backdoor account login
↓
Repeated access to compromised system
```

## SOC Investigation

The SOC analyst should verify:

- whether the account was authorized
- the origin of the login attempt
- what actions were performed during the session

Persistent login activity from unauthorized accounts is a strong indicator of compromise.

