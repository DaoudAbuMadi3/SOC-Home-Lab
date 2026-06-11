# OPNsense Firewall

## Purpose

Acts as the central firewall and network segmentation device for the lab,
controlling traffic between all network zones.

## Network Interfaces

| Interface | Network | Subnet | Role |
|---|---|---|---|
| WAN | NAT | DHCP | Internet access |
| LAN | Internal | 192.168.20.0/24 | Endpoints |
| DMZ | Internal | 192.168.10.0/24 | Web server |
| MGMT | Internal | 192.168.30.0/24 | Splunk SIEM |

## Key Configurations

- Firewall rules restricting inter-zone traffic
- Syslog forwarding to Splunk via UDP 514
- NTP server for all lab VMs
- NAT for internet access

## Logging

Syslog forwarded to Splunk at `192.168.30.124:514`

Captured events:
- Firewall allow/block rules
- NAT translations
- DHCP leases
