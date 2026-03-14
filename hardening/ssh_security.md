```
# SSH Security Hardening

One of the main weaknesses exploited in this attack was password-based SSH authentication.

To reduce this risk, SSH should be hardened using the following controls.

## Disable Password Authentication

Edit the SSH configuration file:
```
sudo nano /etc/ssh/sshd_config
```

change:
```
PasswordAuthentication yes
```
To:
```
PasswordAuthentication no
```
Restart SSH:
```
sudo systemctl restart ssh
```

## Disable Root Login
```
PermitRootLogin no
```

These changes significantly reduce the risk of brute-force attacks.
```
