```
# Attacker Activity Analysis

## Overview

Following successful authentication, the attacker executed several commands that indicate post-compromise activity.

The SOC analyst investigates these actions to determine the attacker’s objectives.

## Observed Actions

The attacker performed the following actions:

1. Privilege escalation using sudo
2. Access to sensitive credential files
3. Creation of a new user account
4. Re-entry using the persistence account

## Privilege Escalation

Below is an evidence of the escalated privilege action performed by the attacker.
![Attacker Privilege Escalation](../screenshots/10_privilege_escalation_sudo_session.png)

This indicates that the attacker gained administrative privileges.

## Credential Access

The attacker accessed the shadow file:
```
cat/etc/shadow
```
This action reveals password hashes stored on the system.

## Persistence

A new account named backdoor was created.

## Command
```
useradd backdoor
```

This allowed the attacker to maintain access to the system.

## Re-entry

The attacker later logged in using the backdoor account.

This confirms that persistence was successfully established.

```
