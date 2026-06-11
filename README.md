# 🛡️ SOC Home Lab — NexaTech Solutions

## Overview

This project documents a fully functional Security Operations Center (SOC) Home Lab
built to simulate a real-world enterprise environment.

The lab is designed to practice threat detection, log analysis, and incident
investigation using industry-standard tools.

---

## 🖥️ Lab Components

| Component | Role |
|---|---|
| OPNsense Firewall | Network segmentation, traffic filtering, syslog forwarding |
| Windows Server 2022 | Active Directory, DNS, Group Policy |
| Windows 10 Pro | Endpoint simulation with Sysmon |
| Ubuntu Web Server | DMZ web server, Apache logs | MySQL Database | DMZ database server, query logging |
| Splunk SIEM | Log aggregation, detection, dashboards, alerts |
| Splunk Universal Forwarder | Log forwarding from endpoints |
| Kali Linux | Attacker machine, attack simulation |

---

## 🌐 Network Architecture

![Network Diagram](/SOC-Home-Lab/Architecture/soc-architecture.png)

---

## 🔀 Network Segmentation

| Network | Subnet | Purpose |
|---|---|---|
| LAN | 192.168.20.0/24 | Internal endpoints |
| DMZ | 192.168.10.0/24 | Web server |
| Management | 192.168.30.0/24 | Splunk SIEM |
| WAN | DHCP | Internet access via NAT |

---

## 📁 Repository Structure

| Folder | Contents |
|---|---|
| `Architecture/` | Network diagrams |
| `Environment-Setup/` | Setup guides per component |
| `Attacks/` | Attack simulations |
| `Detection-Rules/` | Splunk queries and alerts |
| `Investigations/` | Incident investigation cases |

---

## 🎯 Objectives

- Simulate real-world cyber attacks
- Collect and analyze logs via Splunk
- Build detection rules and dashboards
- Perform structured incident investigations
