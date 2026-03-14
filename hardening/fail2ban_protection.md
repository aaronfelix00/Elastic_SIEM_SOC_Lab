```
# Fail2Ban Protection

Fail2Ban protects servers against brute-force attacks by blocking IP addresses that generate repeated authentication failures.

## Install Fail2Ban
```
sudo apt install fail2ban
```

## Enable Fail2ban
```
sudo systemctl enable fail2ban
sudo systemctl start fail2ban
```

Fail2Ban monitors authentication logs and automatically blocks attackers after multiple failed login attempts.
```
