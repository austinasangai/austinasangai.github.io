---
layout: single
title: "How I Set Up My Home Cybersecurity Lab for Under $0"
date: 2024-04-01
categories:
  - blog
tags:
  - home lab
  - kali linux
  - virtualbox
  - beginner
author_profile: true
read_time: true
excerpt: "You don't need expensive hardware to practice cybersecurity. Here's how I built a full attack-and-defend lab using free tools."
---

You don't need to spend any money to start practising offensive and defensive security. This is the exact setup I used to go from beginner to landing my first CTF top-10 finish.

## What you need

- A laptop or desktop with at least 8GB RAM (16GB is better)
- VirtualBox (free) — [download here](https://www.virtualbox.org)
- Kali Linux ISO (free) — [download here](https://www.kali.org)
- DVWA or Metasploitable 2 as a target VM (free)

## Step 1: Install VirtualBox

Download and install VirtualBox for your OS. It's free and runs on Windows, macOS, and Linux.

## Step 2: Set up Kali Linux (attacker machine)

1. Download the Kali Linux VirtualBox image from the official site
2. Import it into VirtualBox (`File → Import Appliance`)
3. Default credentials: `kali / kali`

## Step 3: Set up a vulnerable target

Download **Metasploitable 2** — a deliberately insecure Ubuntu VM perfect for practice.

```bash
# After importing, find its IP
ifconfig
```

## Step 4: Set up an isolated network

In VirtualBox, set both VMs to use a **Host-Only Adapter**. This keeps traffic contained — your attack machine and target can talk to each other, but neither can reach the real internet.

## What to practice

- Nmap scanning against Metasploitable
- Exploiting old services with Metasploit
- Running Nikto against DVWA
- Cracking hashes with John the Ripper

---

This setup has everything you need to follow along with TryHackMe rooms and HackTheBox starting machines. Once you're comfortable, add an ELK Stack VM to start practising log analysis too.

Happy hacking (ethically)!
