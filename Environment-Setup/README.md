# Environment Setup

This section documents the setup and configuration of each component in the
lab — IP addressing, services configured, and how each piece integrates with
Splunk for logging.

| Component | Documentation |
|---|---|
| OPNsense Firewall | [OPNsense.md](OPNsense.md) |
| Active Directory | [ActiveDirectory.md](ActiveDirectory.md) |
| Splunk SIEM | [Splunk.md](Splunk.md) |
| Windows 10 | [Windows10.md](Windows10.md) |
| Web Server | [WebServer.md](WebServer.md) |
| Kali Linux | [Kali.md](Kali.md) |

## Build Order

The lab was built in the following order, which is the recommended order for
anyone replicating it:

1. OPNsense (firewall + network segmentation)
2. Active Directory (Windows Server, OUs, users, GPOs)
3. Windows 10 client (domain-joined endpoint)
4. Web Server (DMZ — Apache + MySQL)
5. Splunk SIEM + Universal Forwarders
6. Kali Linux (attacker machine, added last)
