
# Scanning Phase – Port and Service Enumeration

## Objective
Identify exposed services and assess attack surface within restricted zones.

## Commands Executed

```bash
nmap -sS -T4 10.10.10.0/24
nmap -sS -p 22,80,443 10.10.10.0/24
```

## Observations

-TCP SYN scans generated multiple blocked connection attempts.
- No services were exposed to the PENTEST network.

## Defensive Detection

-Firewall rule triggered: Block lateral movement PENTEST → LAN
-Repeated blocked TCP SYN packets logged.

## SOC Interpretation

This behavior indicates a transition from reconnaissance to active enumeration.
In a production SOC, this would raise the alert priority due to intent escalation.

### Severity - 🟠 Medium
