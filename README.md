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

