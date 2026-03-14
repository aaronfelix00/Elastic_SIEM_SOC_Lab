```
# Investigation Summary

## Incident Overview

The SOC investigation determined that the Ubuntu server was compromised through a successful SSH brute-force attack.

The attacker gained access using valid credentials and performed several post-exploitation activities.

## Key Findings

The attacker performed the following actions:

- brute-force authentication attempts
- successful SSH login
- privilege escalation
- credential dumping
- persistence creation
- system re-entry

## Impact

The attacker obtained administrative access to the system and accessed sensitive credential information.

A persistent backdoor account was also created.

## Conclusion

The incident represents a full compromise of the target host and required immediate containment and remediation.
```
