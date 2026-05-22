---
layout: single
title: "Network Intrusion Detection System"
excerpt: "Built a custom IDS using Python and Scapy to detect port scans, ARP spoofing, and brute force attacks on a home lab network."
date: 2024-03-15
type: blue-team
featured: true
author_profile: false
tags:
  - Python
  - Scapy
  - Wireshark
  - Linux
  - Networking
header:
  teaser: /assets/images/projects/ids.png
---

## Overview

This project involved building a custom Network Intrusion Detection System (NIDS) from scratch using Python and the Scapy library. The system monitors live network traffic and raises alerts when suspicious activity is detected.

## Goals

- Detect port scans (SYN, FIN, NULL, XMAS)
- Identify ARP spoofing / poisoning attacks
- Flag repeated failed SSH/FTP login attempts (brute force)
- Log all alerts to a file with timestamps and source IPs

## Tools & Technologies

| Tool | Purpose |
|------|---------|
| Python 3 | Core scripting language |
| Scapy | Packet capture and analysis |
| Wireshark | Traffic verification and debugging |
| Ubuntu Server | Home lab environment |
| iptables | Supplementary firewall rules |

## Implementation

### 1. Packet capture

```python
from scapy.all import sniff, ARP, TCP

def detect(packet):
    if packet.haslayer(ARP) and packet[ARP].op == 2:
        print(f"[!] ARP Reply from {packet[ARP].psrc} — possible spoofing")
    if packet.haslayer(TCP) and packet[TCP].flags == "S":
        print(f"[!] SYN packet from {packet[IP].src}:{packet[TCP].dport}")

sniff(prn=detect, store=False)
```

### 2. Port scan detection

The system tracks SYN packets per source IP over a rolling 10-second window. If a single IP hits more than 20 different ports within that window, an alert fires.

### 3. ARP spoofing detection

Compares live ARP replies against a trusted IP-to-MAC mapping table built at startup. Any mismatch triggers an alert.

## Results

- Successfully detected Nmap SYN scans, XMAS scans, and NULL scans
- Caught ARP spoofing simulated with `arpspoof`
- Logged 100% of simulated brute force attempts against SSH on port 22

## What I learned

- Deep understanding of TCP/IP layer interactions
- How attackers fingerprint networks using different scan types
- Building detection logic without relying on commercial tools

## Source code

[View on GitHub](https://github.com/yourusername/network-ids)
