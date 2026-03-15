# Credential Dumping

Once root access is obtained, the attacker attempts to extract password hashes from the Linux system.

Linux stores hashed user passwords inside the ```/etc/shadow``` file, which is only accessible to privileged users.

## Command
```
cat/etc/shadow
```

## Evidence
![Shadow File Dump](../screenshots/12_linux_shadow_file_credential_dump.png)

These hashes can potentially be cracked offline to reveal plaintext passwords.

## Security Impact

Accessing ```/etc/shadow``` allows attackers to:

- steal password hashes
- perform offline password cracking
- reuse credentials on other systems
- escalate access further in the environment

## Detection Opportunity

Credential dumping is a strong indicator of compromise and should trigger investigation in a SOC environment.

Relevant indicators include:

- access to ```/etc/shadow```
- root-level commands executed after login

