# 🛡 E️LASTIC SIEM SOC LAB
## 🔍 Detecting and Responding to a Linux SSH Intrusion
-----------------------------------------------------------------------

📘 OVERVIEW

This project demonstrates a complete Security Operations Center (SOC) workflow using the Elastic Stack (Elasticsearch, Kibana, Filebeat).

The lab simulates a realistic cyber intrusion where an attacker compromises a Linux server through an SSH brute-force attack, escalates privileges, dumps credentials, establishes persistence, and reconnects to the system.

The Security Operations Center (SOC) then detects, investigates, and responds to the attack using Elastic SIEM.

Simulated Attack Stages:

🔎 Reconnaissance

🔑 SSH brute force attack

🔓 Unauthorized login

⚡ Privilege escalation

🗝 Credential dumping

🧬 Persistence via backdoor account

🔁 Backdoor re-entry

🕵 SOC investigation

🚨 Incident response

----------------------------------------------------------------------

🎯 OBJECTIVES

The main goals of this SOC lab are:
-  Build a working SIEM monitoring environment
-  Collect and analyze Linux authentication logs
-  Simulate a realistic SSH intrusion scenario
-  Detect malicious behaviour using Elastic Security
-  Investigate alerts using Kibana dashboards
-  Perform incident response and system remediation

---------------------------------------------------------------------

🏗 LAB ARCHITECTURE

The environment consists of three primary systems.

Component                       Role

🐉 Kali Linux                    Attacker machine
🐧 Ubuntu Server            Target host
📊 Elastic Stack               SIEM platform

![Kali Linux](screenshots/01_Kali.png)
![Ubuntu](screenshots/01_Ubuntu.png)
![Elasticsearch_Kibana](screenshots/02_Elasticsearch_Kibana.png)
![Filebeat](screenshots/02_Filebeat.png)

--------------------------------------------------------------------

🗺️ ARCHITECTURE DIAGRAM

The attack telemetry flows through the Elastic monitoring pipeline.

            🐉 Kali Attacker
                   │
                   | SSH Brute Force / Intrusion
                   ▼
            🐧 Ubuntu Server
                   │
                   │ System logs (/var/log/auth.log)
                   ▼
             📦 Filebeat
                   │ Log forwarding
                   ▼
            🔎 Elasticsearch
                   │ Indexed security events
                   ▼
             📊 Kibana SIEM (Elastic Security)
                   │ Dashboards, alerts, investigation
                   ▼
            🕵 SOC Analyst

------------------------------------------------------------------

## ⚔ A️ TTACK SCENARIO

The attacker targets the SSH service exposed on the Ubuntu server.

```mermaid
flowchart TD

A[Reconnaissance]
B[System Logs /var/log/auth.log]
C[SSH Brute Force]
D[Successful Login]
E[Privilege Escalation]
F[Credential Dumping]
G[Persistence Creation]
H[Backdoor Login (Re-entry)]
I[SOC Detection]
J[Incident Investigation]
K[Incident Response (Remediation)]

A -->|🔎| B
B -->|📄| C
C -->|🔑| D
D -->|🔓| E
E -->|⚡| F
F -->|🗝️| G
G -->|🧬| H
H -->|🔁| I
I -->|🚨| J
J -->|🕵️| K
K -->|🛠️| L[End]
```
------------------------------------------------------------------

🧰 TOOLS DEPLOYED

Tool                                Purpose

🐉 Kali Linux                 Attack platform
💣 Hydra                       SSH brute force
🔐 SSH                         Remote login
📦 Filebeat                    Log collection
🔎 Elasticsearch            Log storage
📊 Kibana                      Visualization
🛡 Elastic Security         Threat Detection

-----------------------------------------------------------------

📂 LOG SOURCES MONITORED

/var/log/auth.log
        │
        ▼
SSH authentication events
        │
        ▼
Privilege escalation logs
        │
        ▼
User account changes
        │
        ▼
Credential access attempts

-----------------------------------------------------------------

🚨 ATTACK EXECUTION

-----------------------------------------------------------------
🔎 1. Reconnaissance

The attacker begins by scanning the target system.
```
nmap -sV "Target IP"
```
Workflow

🐉 Kali Attacker
      │
      ▼
🔎 Port Scan
      │
      ▼
SSH Service Detected

![Recon](screenshots/05_Attacker_Recon_nmap_scan.png)

🔑 2. SSH Brute Force

The attacker attempts to guess passwords.
```
hydra -L users.txt -P passwords.txt ssh://"Target IP"
```
Workflow

💣 Hydra Attack
      │
      ▼
Multiple Failed Logins
      │
      ▼
📄 auth.log Entries
      │
      ▼
🚨 SIEM Detection

![Hydra Execution](screenshots/06_ssh_bruteforce_attack_execution_with_hydra.png)
![Failed SSH Attempts](screenshots/07_multiple_failed_ssh_authentication_attempts.png)

🔓 3. Successful Login

Eventually a password is discovered.
```
ssh "username"@"Target IP"
```
Workflow

Failed Logins
      │
      ▼
Correct Password Found
      │
      ▼
Successful Authentication
      │
      ▼
Unauthorized Access

![Succesful Login](screenshots/08_successful_ssh_authentication_event.png)

⚡ 4. Privilege Escalation

The attacker escalates privileges.
```
sudo -i
```
Workflow

  User Shell
      │
      ▼
⚡ sudo command
      │
      ▼
👑 Root Access

Indicator in logs:
```
sudo session opened
```
This indicates the attacker now has full administrative control.

![Privilege Escalation](screenshots/10_privilege_escalation_sudo_session.png)


🗝️ 5. Credential Dumping

The attacker accesses the password hash database.

cat /etc/shadow

Workflow

👑 Root Access
      │
      ▼
Sensitive File Access
      │
      ▼
Password Hash Extraction

MITRE ATTACK
```
T1003 Credential Dumping
```
![Credential Dumping](screenshots/12_linux_shadow_file_credential_dump.png)


🧬 6. Persistence Creation

The attacker creates a backdoor user.
```
useradd backdoor
passwd backdoor
```
Workflow

Root Access
      │
      ▼
New User Created
      │
      ▼
Backdoor Account
      │
      ▼
Persistent Access

![Backdoor Creation](screenshots/14_backdoor_account_creation_command.png)


🔁 7. Backdoor Re-entry

The attacker reconnects later.
```
ssh backdoor@"Target IP"
```
Workflow

Backdoor Credentials
      │
      ▼
SSH Authentication
      │
      ▼
Persistent Access

![Backdoor Persistence](screenshots/16_backdoor_ssh_login_persistence_access.png)

-------------------------------------------------------------------

🛡 DETECTION ENGINEERING

The SOC configured detections for multiple attack behaviours.

![Auth Analysis](screenshots/authentication_analysis.png)

-------------------------------------------------------------------

🚨 A. SSH Brute Force Detection

Indicator:
```
event.outcome: "failure"
```
Vector:

Multiple Failures
      │
      ▼
Threshold Triggered
      │
      ▼
🚨 Alert Generated


🔓 B. Successful Login Detection

Indicator:
```
event.outcome: "success"
```
Vector:

Successful Login
      │
      ▼
User Activity Investigation


⚡ C. Privilege Escalation Detection

Indicator:
```
sudo usage
```
Vector:

User Command
      │
      ▼
⚡ sudo invocation
      │
      ▼
Root Privileges


🧬 D. Suspicious User Creation

Indicator:
```
useradd
```
Vector:

New User Created
      │
      ▼
Potential Persistence


🗝  E. Credential Access Detection

Indicator:
```
/etc/shadow
```
Vector:

Sensitive File
      │
      ▼
Credential Dump Attempt

![Timeline Analysis](screenshots/20_SIEM_attack_timeline_analysis.png)

------------------------------------------------------------------

🕵️ SOC INVESTIGATION WORKFLOW

🚨 Alert Triggered
      │
      ▼
Review Failed Logins
      │
      ▼
Identify Successful Login
      │
      ▼
Investigate Privilege Escalation
      │
      ▼
Detect Credential Dumping
      │
      ▼
Identify Persistence
      │
      ▼
Contain Attacker

----------------------------------------------------------------

⏱ INCIDENT TIMELINE(EXCERPTS)

Time              Event                                     Interpretation                                               

20:35             SSH authentication failures               Brute-force attempts begins
20:48             sudo escalation                           Privilege escalation                                                                                                          
21:03             backdoor account                          Persistence established                                                                                  
21:07             login attempts with backdoor              Persistence tested    
21:08             Systemd session confirmed                 Backdoor access confirmed    

![Timeline Analysis](screenshots/20_SIEM_attack_timeline_analysis.png)
                                                                                    
-----------------------------------------------------------------

🚑 INCIDENT RESPONSE

Terminate attacker session:
```
pkill -u backdoor
```
Remove persistence:
```
userdel -r backdoor
```
Delete home directory:
```
rm -rf /home/backdoor
```
Verify removal:
```
cat /etc/passwd | grep backdoor
```
![Backdoor Termination](screenshots/22_backdoor_termination_removal_and_validation.png)

-----------------------------------------------------------------

🔒 HARDENING MEASURES

Security Controls
      │
      ├── 🔐 SSH Hardening
      ├── 🛑 Fail2ban
      ├── 🧱 Firewall
      ├── 🔑 Password Policy
      └── 📊 Continuous Monitoring

Recommended improvements:
- Disable password SSH authentication
- Enable SSH key authentication
- Install Fail2ban
- Enable firewall
- Disable root login

![Fail2ban](screenshots/23_fail2ban_status_verification.png)
![Firewall](screenshots/24_firewall_security_rules_enabled.png)
![Re-entry Failure](screenshots/25_confirmation_of_reentry_failed.png)

------------------------------------------------------------------

🎯 MITRE ATT&CK Mapping

Tactic                           Technique

Discovery                    Network Service Discovery
Credential Access       Brute Force
Initial Access               Valid Accounts
Privilege Escalation    sudo abuse
Credential Access       Credential Dumping
Persistence                 Create Account
Persistence                 Account Manipulation

-------------------------------------------------------------------

🧠 Skills Demonstrated

This project demonstrates practical SOC analyst skills including:
- SIEM engineering
- Linux log analysis
- threat detection
- incident investigation
- incident response
- MITRE ATT&CK mapping

Skills gained:

- Elastic SIEM configuration
- Linux log analysis
- SSH brute force detection
- Persistence investigation
- Incident response procedures
- Threat mapping using MITRE ATT&CK

------------------------------------------------------------------

📚 LESSONS LEARNED

Key insights from the lab:

- SSH brute-force attacks are easily visible with centralized logging
- Credential dumping creates strong detection signals
- Persistence through user accounts is detectable
- SIEM dashboards greatly accelerate investigations

-----------------------------------------------------------------

🏁 CONCLUSION

This project demonstrates a complete SOC detection and response workflow 
using Elastic SIEM.

It highlights the importance of:

- centralized logging
- detection engineering
- investigation workflows
- incident response
