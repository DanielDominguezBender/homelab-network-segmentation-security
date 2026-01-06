# Reconnaissance Phase – Internal Network

## Objective
Identify reachable hosts and network boundaries from a compromised internal segment.

## Attacker Context
- Host: Kali Linux
- Network: PENTEST (10.10.20.0/24)
- Gateway: 10.10.20.1 (pfSense)

## Commands Executed

```bash
ip a
ip route
arp-scan -l
nmap -sn 10.10.10.0/24
```

## Observations

- Network and gateway configuration validated.
- ICMP sweep towards the Trusted LAN triggered firewall blocks.
- No hosts in LAN responded directly to ICMP requests.

## Defensive Detection

- Firewall rule triggered: Block lateral movement PENTEST → LAN
- Multiple ICMP packets blocked and logged.
- Pattern consistent with internal reconnaissance.

## SOC Interpretation

This activity represents an early attack phase aimed at discovering internal assets.
While no compromise occurred, this behavior would be classified as suspicious and monitored closely.

### Severity - 🟡 Low–Medium (Reconnaissance)
