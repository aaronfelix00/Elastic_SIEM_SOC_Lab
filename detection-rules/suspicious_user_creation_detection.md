```
## Overview

Attackers often create new user accounts to maintain persistence on compromised systems.

Monitoring account creation events is therefore an important security control.

## Command Used by Attacker
```
useradd backdoor
```

A password may then be set:
```
passwd backdoor
```

## Dectection Indicator
![Detection Indicator](../screenshots/14_backdoor_account_creation_command.png)

## Verification
The new account appears in:
```
/etc/passwd
```
![Verification of account created](../screenshots/15_backdoor_account_visible_in_passwd_file.png)

## Detection Pattern
Suspicious sequence:
Root access obtained
↓
New user created
↓
Persistence established

## SOC Investigation

The SOC analyst should determine:

- whether the account was authorized
- when the account was created
- which user created the account

Unauthorized account creation is a strong indicator of persistence.
```
