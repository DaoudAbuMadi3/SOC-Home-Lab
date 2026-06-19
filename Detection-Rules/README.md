# 🔍 Detection Rules

This folder contains the Splunk detection rules (SPL searches configured as
alerts) built for the lab. Each rule maps to a specific attack technique in
[Attacks/](../Attacks/README.md).

## Indexes

| Index | Source |
|---|---|
| `main` | General/default events |
| `opnsense` | Firewall logs (syslog) |
| `web_logs` | Apache access/error logs (DMZ web server) |

## Alert Catalog

| Alert | Index/Source | Trigger Logic | Severity |
|---|---|---|---|
| SSH Brute Force | `opnsense` / auth logs | Repeated failed SSH auth attempts from same source IP within a short window | High |
| Port Scan Detection | `opnsense` | Single source IP hitting many distinct destination ports in a short window | Medium |
| Web Attack (SQLi/XSS) | `web_logs` | Request patterns matching SQL injection or script-injection signatures | High |
| MySQL Query Spike | `main` | Abnormal spike in query volume/rate compared to baseline | Medium |
| DoS / Flood Detection | `opnsense` | High volume of connections/packets from a single source in a short window | High |

Each rule will get its own file with the full SPL query, schedule, and
threshold once finalized — e.g. `ssh-bruteforce.spl`.

## SPL Query Template

```spl
index=<index_name> sourcetype=<sourcetype>
| <filtering/aggregation logic>
| where <threshold_condition>
```

## Notes

- All alerts are configured to trigger on a real-time or near-real-time
  schedule unless otherwise noted.
- Thresholds are tuned against this lab's traffic baseline and may need
  adjustment for different environments.
