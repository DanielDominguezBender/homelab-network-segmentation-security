
# Infrastructure Targeting – Firewall Enumeration

## Objective
Probe critical network infrastructure for exposed services or weaknesses.

## Target
- pfSense firewall
- Interface: PENTEST (10.10.20.1)

## Command Executed

```bash
nmap -A 10.10.20.1
```

## Observations

-Fingerprinting attempts blocked.
-No management services exposed to the PENTEST zone.

## Defensive Detection

-Firewall rule triggered: Protect pfSense from PENTEST
-Multiple blocked TCP and ICMP packets logged.

## SOC Interpretation

Direct attacks against network infrastructure are considered high-risk events.
Even unsuccessful attempts are strong indicators of malicious intent.

### Severity - 🔴 High
