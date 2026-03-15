# Successful SSH Login

After multiple authentication attempts during the brute-force attack, the attacker eventually discovers valid credentials for a user account on the Ubuntu server.

This marks the moment when the attacker gains initial access to the target system.

## Command
```
ssh "username"@"Target IP"
```
The attacker enters the correct password obtained during the brute-force process.

## Expected Result

If authentication succeeds, the attacker receives an interactive shell on the Ubuntu system.

![Successful SSH Attempt](../screenshots/08_successful_ssh_authentication_event.png)
![Successful SSH Attempt Event logged in Kibana](../screenshots/09_successful_login_event_in_kibana_discover.png)

