# Privilege Escalation

After gaining access to the Ubuntu system through SSH, the attacker escalates privileges to obtain root access.

Root access allows the attacker to perform administrative actions such as modifying users, accessing protected files, and establishing persistence.

## Command
```
sudo -i
```

## Explanation

The 'sudo -i' command opens a root login shell if the user has sudo privileges and provides the correct password.

The shell prompt changes from a user context to root.

![Privilege Escalation](../screenshots/10_privilege_escalation_sudo_session.png)

This indicates that the attacker now has full administrative control of the system.

## Log Evidence

Ubuntu logs this activity in:
```
/var/log/auth.log
```

## Example entry:
```
sudo: pam_unix(sudo-i:session): session opened for user root by ragnar(uid=1000)
```

This event is visible in Elastic SIEM and indicates privilege escalation activity.

