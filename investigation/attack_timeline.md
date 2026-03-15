## Overview

After confirming that a successful login occurred, the SOC analyst reconstructs the sequence of events that took place on the compromised system.

Timeline reconstruction helps determine how the attacker moved through the environment.

## Observed Event Sequence

Reconnaissance
↓
SSH brute-force attack
↓
Successful authentication
↓
Privilege escalation
↓
Credential dumping
↓
Persistence creation
↓
Backdoor login

## Evidence
![Attack Timeline Extract](../screenshots/20_SIEM_attack_timeline_analysis.png)

## Purpose

Timeline reconstruction allows the SOC team to understand:

- the scope of the intrusion
- the attack progression
- the impact on the system

