# Home SOC Lab Project

## Overview  
This project documents the setup of a Home Security Operations Center (SOC) using Splunk, a Windows VM, and Kali Linux to simulate and detect malicious activity.

### Before:
- A basic home lab with no SIEM or detection capabilities.

### After:  
- Splunk Enterprise and Universal Forwarder configured.  
- Dashboards built to detect attacks simulated from Kali Linux.  
- Logs from Windows VM ingested and searchable in Splunk.

---

## Technology Utilized  
- Splunk Enterprise – Installed on macOS for log aggregation and analysis  
- Splunk Universal Forwarder – Installed on Windows VM for event log forwarding  
- Sysmon – Provides enhanced visibility into Windows processes  
- Kali Linux – Used to simulate attacker behavior (brute-force, enumeration, etc.)  
- VMware Fusion – Runs both Kali and Windows VMs on Mac

---

## Table of Contents  
1. [Lab Architecture](#lab-architecture)  
2. [Splunk Setup](#splunk-setup)  
3. [Forwarder Configuration](#forwarder-configuration)  
4. [Simulated Attacks](#simulated-attacks)  
5. [Dashboards and Detection](#dashboards-and-detection)  
6. [Lessons Learned](#lessons-learned)

---

## 1. Lab Architecture  
```
Host (macOS)
├── Splunk Enterprise (192.168.x.x)
├── Kali Linux VM
└── Windows 11 VM (Splunk UF + Sysmon)
```
- All devices are on the same internal virtual network.

---

## 2. Splunk Setup  
- Splunk Enterprise installed on the host Mac  
- Configured receiving on TCP port 9997  
- Created custom dashboards for event analysis

---

## 3. Forwarder Configuration  
- Installed Splunk Universal Forwarder on Windows  
- Configured inputs for:
  - Windows Security Event Logs (4624, 4625, 4688, etc.)
  - Sysmon logs
- Confirmed connectivity using:
  ```bash
  splunk list forward-server
  splunk list monitor
  ```

---

## 4. Simulated Attacks  
Attacks from Kali Linux used to test detection capabilities:

### Information Gathering
```
nmap -sC -sV -Pn <target>
```

### Brute Force
```
crackmapexec smb <target> -u administrator -p rockyou.txt
hydra -t 4 -V -f -l administrator -P rockyou.txt rdp://<target>
```

---

## 5. Dashboards and Detection  
Dashboards created in Splunk include:

- Top Failed Login Attempts – EventCode=4625
- Successful Logins by User – EventCode=4624
- Suspicious PowerShell Activity – EventCode=4104
- Process Creation Monitoring – EventCode=4688
- SMB Share Access – EventCode=5140
- New Local Admin Accounts – EventCodes=4720, 4732, 4728

---

## 6. Lessons Learned  
- Building a SOC does not require enterprise hardware, just planning.  
- Simulated attacks provide valuable insight into log behavior.  
- Sysmon adds deep visibility for Windows monitoring.  
- Splunk dashboards can be customized for specific attacker behaviors.

---



## Connect  
[LinkedIn - Kency Francois](https://linkedin.com/in/kency-francois)

---
