# ⚔️ Attack Simulations

This folder documents each attack exercise performed against the lab,
starting simple and growing in complexity over time. Every attack entry is
paired with the detection rule that should (or did) catch it — see
[Detection-Rules/](../Detection-Rules/README.md).

## Methodology

1. **Simulate** — run the attack from Kali against the DMZ web server
2. **Detect** — confirm whether the relevant Splunk alert fired
3. **Document** — record commands used, logs generated, and outcome
4. **Iterate** — refine the attack or the detection rule and repeat

## Exercise Log

| # | Attack | Target | Detection Rule | Status |
|---|---|---|---|---|
| 1 | SSH Brute Force (Hydra) | DMZ Web Server | SSH Brute Force Alert | ⏳ Planned |
| 2 | Port Scan (Nmap) | DMZ Web Server | Port Scan Detection Alert | ⏳ Planned |
| 3 | SQL Injection | Web Application | SQLi/XSS Alert | ⏳ Planned |
| 4 | Cross-Site Scripting (XSS) | Web Application | SQLi/XSS Alert | ⏳ Planned |
| 5 | MySQL Query Spike | Database | MySQL Spike Alert | ⏳ Planned |
| 6 | DoS (hping3) | DMZ Web Server | Web Attack Alert | ⏳ Planned |

> Status legend: ⏳ Planned · 🟡 In Progress · ✅ Completed & Documented

Each completed exercise gets its own file in this folder, e.g.
`01-ssh-bruteforce.md`, following the template below.

## Write-up Template

```markdown
# Attack: <name>

## Objective
What this attack simulates and why.

## Attacker Tool & Command
The exact command(s) run from Kali.

## Target
IP, service, and port targeted.

## Expected Detection
Which Splunk alert/rule should trigger.

## Result
Did the alert fire? Screenshot/log excerpt of the triggered alert.

## Lessons Learned
What worked, what didn't, what was tuned afterward.
```
