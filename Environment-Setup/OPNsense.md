# OPNsense Firewall

## Purpose

Acts as the central firewall and network segmentation device for the lab,
enforcing least-privilege traffic rules between every network zone and
forwarding logs to Splunk for monitoring.

## Network Interfaces

| Interface | Network | Subnet | Role |
|---|---|---|---|
| WAN | Bridged | 192.168.1.0/24 (host network) | Internet access + external attacker (Kali) |
| LAN | Internal (`intnet_lan`) | 192.168.20.0/24 | Endpoints (AD, Windows 10) |
| OPT1 (DMZ) | Internal (`intnet_dmz`) | 192.168.10.0/24 | Web server |
| OPT2 (MGMT) | Internal (`intnet_mgmt`) | 192.168.30.0/24 | Splunk SIEM |

## Key Firewall Rules (Summary)

**WAN**
- Allow all → Web Server (HTTP/HTTPS) — simulates public-facing access
- Allow Ubuntu management host → Web/Splunk/OPNsense for SSH & admin access
- Block all other access to OPNsense WebGUI and Splunk WebUI from WAN

**OPT1 (DMZ)**
- Allow any → Web Server (HTTP/HTTPS)
- Allow Web Server → Splunk (port 9997) — log forwarding only
- Block SSH access to Web Server except from the management host
- Block all DMZ access to OPNsense WebGUI
- Default deny on all other traffic

**OPT2 (MGMT / Splunk)**
- Allow management host → Splunk WebUI (8000) and SSH
- Allow all → Splunk Forwarder port (9997)
- Block Splunk API (8089) and OPNsense WebGUI from this zone
- Default deny on all other traffic

**LAN**
- Allow LAN → Internet (HTTP/HTTPS), excluding internal network ranges
- Allow Windows 10 → AD (DNS, Kerberos, LDAP, SMB)
- Block LAN access to Splunk WebGUI; allow only the forwarder port (9997)
- Default deny on all other traffic

> Full rule sets per interface are screenshotted and stored in
> `Architecture/firewall-rules/` for reference.

## NTP

OPNsense acts as the NTP server for all VMs, synced against the
`opnsense.pool.ntp.org` pool and serving time across LAN, OPT1, OPT2, and WAN
interfaces.

## Logging

Firewall logs are forwarded to Splunk for indexing and alerting.

Captured events:
- Firewall allow/block decisions per rule
- NAT translations
- DHCP leases

## Notes on Attacker Placement

Kali Linux is connected via the WAN-side **Bridged Adapter**, putting it on
the same network as the physical host (192.168.1.0/24) rather than inside
any internal segment. This intentionally simulates an **external attacker**
on the internet targeting the DMZ web server, rather than an insider threat.
