# 🛡️ Secure Home Lab – Network Segmentation, Pentesting & SOC Mindset

This project documents the design and implementation of a **secure and realistic home lab** focused on **network segmentation, firewalling, attack simulation and security monitoring**.

The goal of the lab is not to deploy tools blindly, but to **understand how attacks look from both Red Team and Blue Team perspectives**, using realistic constraints and consumer-grade hardware.

---

## 🎯 Objectives

- Design a segmented network with **clear trust boundaries**
- Prevent **lateral movement** between internal zones
- Simulate realistic **internal attack scenarios**
- Observe and interpret security events as a **SOC analyst**
- Build a lab that can be **extended with SIEM and virtualization**

---

## 🧱 Architecture Overview

The lab is structured around **three isolated network zones**, all routed through a central pfSense firewall:

| Zone | Subnet | Trust Level |
|----|----|----|
| WAN | ISP network | Untrusted |
| LAN (Trusted) | 10.10.10.0/24 | High |
| PENTEST | 10.10.20.0/24 | Hostile |

All inter-zone traffic is explicitly filtered and logged.

```text
                 Internet
                    │
            [ ISP Router ]
                    │
             [ pfSense FW ]
              ├───────────┐
              │           │
     LAN (Trusted)     PENTEST (Hostile)
     10.10.10.0/24     10.10.20.0/24
          │                 │
     Admin / Tools        Kali Linux
```


---

## 🔐 Firewall & Segmentation Strategy

The **PENTEST network is treated as compromised by design**.

Core security rules:

- ❌ PENTEST → LAN (blocked, logged)
- ❌ PENTEST → pfSense management (blocked, logged)
- ✅ PENTEST → Internet (allowed, logged)
- ✅ LAN → pfSense management (allowed)
- ❌ WAN → internal networks (default deny)

ICMP access to pfSense was enabled **only for diagnostics**, and documented as non-production behavior.

---

## ☠️ Attack Simulation

From the PENTEST zone (Kali Linux), the following attack phases were simulated:

### Reconnaissance
- ARP discovery
- ICMP sweep (`nmap -sn`)

➡️ Detected as lateral movement attempts.

### Scanning
- TCP SYN scans
- Focused service enumeration

➡️ Detected via repeated blocked connections.

### Infrastructure Targeting
- Fingerprinting attempts against pfSense

➡️ Logged as high-risk events targeting critical infrastructure.

---

## 🧠 Detection & SOC Analysis

Instead of focusing only on blocking traffic, the lab emphasizes **visibility and correlation**.

Observed patterns:
- Repeated connection attempts from a single internal host
- Sequential attack phases (recon → scan → targeting)
- Clear distinction between benign diagnostics and malicious behavior

Even without a full SIEM, **manual correlation of firewall logs** allowed accurate identification of attack chains, mirroring real SOC workflows.

---

## 🔎 Key Learnings

- Network segmentation is one of the most effective security controls
- Logs without context are noise; **correlation creates insight**
- Not all traffic should be blocked — some must be observed
- ICMP is a diagnostic tool, not a security objective
- A firewall is both a **control** and a **sensor**

---

## 🚀 Roadmap – Part II

Planned extensions:

- SIEM integration (Wazuh)
- Advanced detection rules
- Alerting and correlation
- Infrastructure virtualization with Proxmox

---

## ⚠️ Disclaimer

All attacks were performed in a **controlled lab environment**.  
No external systems or networks were targeted.
