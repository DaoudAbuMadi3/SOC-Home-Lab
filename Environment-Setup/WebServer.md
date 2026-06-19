# Ubuntu Web Server — DMZ

## Purpose

Public-facing web application server placed in the DMZ to act as the
primary attack target, simulating an internet-exposed enterprise web
service.

## Machine Details

| Property | Value |
|---|---|
| OS | Ubuntu Server |
| IP Address | 192.168.10.181 |
| Network | DMZ (192.168.10.0/24) |
| Services | Apache (HTTP/HTTPS), MySQL |

## Services

- **Apache** — serves the web application on ports 80/443
- **MySQL** — backend database with query logging enabled, used to detect
  abnormal query volume (SQL injection attempts, automated scanning)

## Logging Integration

Splunk Universal Forwarder installed and configured to forward:
- Apache access logs → `web_logs` index
- Apache error logs → `web_logs` index
- MySQL query logs → `main` index

## Firewall Access (from OPNsense — DMZ/OPT1 rules)

| Source | Destination | Port | Purpose |
|---|---|---|---|
| Any (WAN) | Web Server | 80, 443 | Public web access (incl. simulated attacker traffic) |
| Web Server | Splunk (192.168.30.124) | 9997 | Log forwarding only |
| Management host | Web Server | 22 (SSH) | Administrative access |
| — | Web Server | 22 (SSH) | Blocked from all other sources |

The DMZ is intentionally restricted to **outbound log forwarding only**
toward the Management zone — it cannot reach the LAN or AD, enforcing
network segmentation even if the web server itself is compromised.
