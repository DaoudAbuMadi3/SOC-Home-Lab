# Active Directory — Windows Server 2022

## Purpose

Provides centralized identity, authentication, and policy management for
the LAN zone, simulating a typical enterprise domain environment.

## Server Details

| Property | Value |
|---|---|
| Role | Domain Controller, DNS |
| IP Address | 192.168.20.190 |
| Network | LAN (192.168.20.0/24) |

## Organizational Units (OUs)

Four OUs were created to logically separate users/resources by department
or function (e.g., IT, HR, Management, Servers — adjust naming as built).

## Users & Groups

- **12 domain users** created across the OUs
- **4 security groups** mapping to department/role-based access

## Group Policy Objects (GPOs)

| GPO | Purpose |
|---|---|
| Password Policy | Enforces minimum complexity/length and expiration rules |
| USB Block | Disables removable storage devices on domain endpoints |
| Audit Logging | Enables security event auditing for logon/logoff and object access |

All GPOs were verified by applying them to the domain-joined Windows 10
client and confirming enforcement (`gpresult` / `gpupdate /force`).

## Logging Integration

Security and authentication events are forwarded via the Splunk Universal
Forwarder to the `main` index in Splunk, including:
- Logon/logoff events
- Account lockouts and failed authentication attempts
- GPO application events

## Firewall Access (from OPNsense)

| Source | Destination | Port | Purpose |
|---|---|---|---|
| Windows 10 (192.168.20.150) | AD (192.168.20.190) | 53 (DNS) | Name resolution |
| Windows 10 | AD | 88 (Kerberos) | Authentication |
| Windows 10 | AD | 389 (LDAP) | Directory queries |
| Windows 10 | AD | 445 (SMB) | File/policy access |
