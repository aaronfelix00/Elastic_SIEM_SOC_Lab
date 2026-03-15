# Firewall Configuration

A firewall can reduce exposure by limiting access to critical services.

Ubuntu uses UFW (Uncomplicated Firewall).

## Enable Firewall
```
sudo ufw enable
```

## Allow SSH
```
sudo ufw allow ssh
```

## Check Firewall Status
```
sudo ufw status
```

Restricting access reduces the attack surface of the system.

