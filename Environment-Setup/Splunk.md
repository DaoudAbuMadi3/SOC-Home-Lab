# Splunk SIEM

## Purpose

Central log aggregation and detection platform for the entire lab. Collects
logs from OPNsense, the DMZ web server, Active Directory, and Windows 10,
and runs the detection rules documented in
[Detection-Rules/](../Detection-Rules/README.md).

## Server Details

| Property | Value |
|---|---|
| IP Address | 192.168.30.124 |
| Network | Management (192.168.30.0/24) |
| Web UI Port | 8000 |
| Forwarder Listening Port | 9997 |
| API Port (restricted) | 8089 |

## Indexes

| Index | Purpose |
|---|---|
| `main` | Windows/AD events, general logs |
| `opnsense` | Firewall and network logs |
| `web_logs` | Apache access/error logs from the DMZ web server |

## Data Inputs

Logs are collected via the **Splunk Universal Forwarder**, installed on:
- Windows Server (AD)
- Windows 10 client
- Ubuntu DMZ web server

Configuration involved resolving `inputs.conf` path issues, service account
permission fixes, and correcting log path mismatches across the different
sources.

## Dashboards

| Dashboard | Content |
|---|---|
| OPNsense Overview | Firewall allow/block trends, top blocked sources, NAT activity |
| Web Server Overview | Apache request volume, response codes, top requested URIs |

## Alerts

Five detection alerts were built and validated against live traffic
(see [Detection-Rules/README.md](../Detection-Rules/README.md) for full
catalog):
1. SSH Brute Force
2. Web Attack detection
3. SQL Injection / XSS detection
4. MySQL query spike
5. Port scan detection

## Operational Notes

- Disk space exhaustion was previously resolved by expanding the VM's
  virtual disk and extending the LVM filesystem.
- Periodic `clean eventdata` is used to reset indexed events between testing
  cycles without affecting saved searches, dashboards, or alert
  configurations (those live under `etc/apps`, not the index itself).
