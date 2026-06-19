# Kali Linux — Attacker Machine

## Purpose

Represents an **external threat actor** used to simulate real-world attacks
against the DMZ web server, generating the traffic that the Splunk
detection rules are built to catch.

## Machine Details

| Property | Value |
|---|---|
| OS | Kali Linux |
| Network Adapter | Bridged Adapter |
| Network | 192.168.1.0/24 (host's physical network) |

## Why Bridged, Not Internal

Unlike every other VM in the lab — which sits on an isolated internal
network (LAN/DMZ/MGMT) — Kali is connected via a **Bridged Adapter**,
placing it on the same network segment as the physical host rather than
inside the lab's internal topology.

This is a deliberate design choice: it simulates an **attacker on the
internet/WAN side** attempting to reach a publicly exposed service, the
same way a real attacker would target an internet-facing web server,
rather than simulating an insider threat already inside the network.

```
Kali (Bridged, 192.168.1.x)  →  OPNsense WAN  →  DMZ Web Server (192.168.10.181)
        "External Attacker"                         "Public-facing target"
```

## Tooling Used

| Tool | Purpose |
|---|---|
| Nmap | Reconnaissance, port scanning |
| Hydra | SSH brute force |
| sqlmap | SQL injection testing |
| hping3 | DoS/flood testing |

## Notes

- A GRUB boot failure on this VM was previously resolved.
- Planned migration: moving the Kali VDI from HDD to SSD with a fresh 20GB
  install for improved performance.
- Attack activity from this machine is documented per-exercise in
  [Attacks/](../Attacks/README.md).
