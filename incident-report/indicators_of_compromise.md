## Overview

This document lists the key indicators of compromise (IOCs) identified during the simulated SSH intrusion.

These indicators help the SOC analyst identify malicious activity, correlate events, and determine the scope of compromise.

## Network Indicators

### Attacker Source IP

The attacker originated from the Kali Linux machine.

## Evidence
```
10.0.0.99
```
This IP was associated with:
	• repeated failed SSH logins
	• successful authentication
	• post-compromise activity

## Account Indicators

### Compromised Account
```
ragnar
```
This account was used for the initial successful SSH login.

### Persistent Account
```
backdoor
```
This account was created by the attacker to maintain access to the system.

## Log Indicators
The following log patterns indicate compromise:

### Failed SSH Authentication Attempts
```
Failed password for invalid user admin
Failed password for ragnar
```  

### Successful SSH Authentication
```
Accepted password for ragnar
Accepted password for backdoor
```

### Privilege Escalation
```
sudo: session opened for user root
```

### Persistence Creation
```
useradd backdoor
passwd: password changed for backdoor
```

### Sensitive File Access
```
cat /etc/shadow
```

## File and System Indicators

### Sensitive File Accessed
```
/etc/shadow
```
This indicates credential dumping activity

### User Database Modified
```
/etc/passwd
```
The backdoor account appeared in this file.

![Evidence of backdoor account](../screenshots/15_backdoor_account_visible_in_passwd_file.png)

### Persistence Artifacts
Potential persistence-related artifacts include:
```
/home/backdoor
/home/backdoor/.ssh
authorized_keys
```

## Behavorial Indicators
The following attacker behaviors were observed:
	• brute-force password guessing
	• successful SSH compromise
	• privilege escalation
	• credential dumping
	• unauthorized user creation
	• persistent re-entry using the backdoor account

## SOC Relevance
These indicators provide strong evidence of system compromise and should be used for:
	• incident triage
	• timeline reconstruction
	• scoping the intrusion
	• containment and eradication

## Summary

The strongest indicators of compromise in this lab were:
	• repeated failed SSH logins from the attacker IP
	• successful login after brute-force attempts
	• sudo privilege escalation
	• access to /etc/shadow
	• creation and use of the backdoor account

