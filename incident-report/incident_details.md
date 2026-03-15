## Attack Vector

The attacker targeted the SSH service exposed on the Ubuntu server.

Using Hydra, the attacker attempted multiple username and password combinations until valid credentials were discovered.

## Compromise

The attacker successfully logged into the system using the compromised account.

After login, the attacker escalated privileges using sudo.

## Post-Exploitation

Once root access was obtained, the attacker performed the following actions:

- accessed the ```/etc/shadow``` file
- created a persistent backdoor account
- reconnected using the persistence account

## Detection

Elastic SIEM detected suspicious authentication behavior including multiple failed login attempts followed by a successful authentication event.

This triggered a SOC investigation.

