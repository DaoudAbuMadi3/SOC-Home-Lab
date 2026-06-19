# Windows 10 Pro — Endpoint Client

## Purpose

Simulates a typical domain-joined corporate endpoint inside the LAN zone,
used to validate Active Directory policies and generate endpoint telemetry.

## Machine Details

| Property | Value |
|---|---|
| IP Address | 192.168.20.150 |
| Network | LAN (192.168.20.0/24) |
| Domain-joined | Yes — joined to the NexaTech AD domain |

## Configuration

- Joined to the domain and placed in its corresponding OU
- GPOs applied and verified (Password Policy, USB Block, Audit Logging)
- Splunk Universal Forwarder installed to forward Windows Event Logs

## Logging Integration

Forwards the following to Splunk (`main` index):
- Security event log (logons, failed logons, account lockouts)
- System and application event logs
- GPO application results

## Firewall Access (from OPNsense — LAN rules)

| Destination | Port | Purpose |
|---|---|---|
| AD (192.168.20.190) | 53, 88, 389, 445 | DNS, Kerberos, LDAP, SMB |
| Web Server (192.168.10.181) | 80, 443 | Access to DMZ web application |
| Internet | 80, 443 | General browsing (excluding internal ranges) |

> Direct access to the Splunk Web UI (port 8000) from LAN is blocked; only
> the forwarder port (9997) is permitted.
