---
title: "CTF Name - Machine/Challenge Name"
date: 2026-03-10
draft: false
description: "Writeup for Machine/Challenge Name on CTF Platform. Covers enumeration, exploitation and privilege escalation."
tags: ["ctf", "hackthebox", "linux", "easy"]
categories: ["CTF"]
series: ["HackTheBox"]
showToc: true
TocOpen: true
cover:
  image: ""
  alt: "Machine/Challenge Name"
---

## Box Info

| Field | Details |
|-------|---------|
| **Platform** | HackTheBox / TryHackMe |
| **Box Name** | Machine Name |
| **OS** | Linux / Windows |
| **Difficulty** | Easy / Medium / Hard / Insane |
| **IP** | 10.10.10.x |
| **Release Date** | YYYY-MM-DD |
| **Retired** | Yes / No |

---

## Summary

Brief 2-3 sentence overview of the box. What was the attack path? What made it interesting or unique? No spoilers yet, just a high level overview.

---

## Recon

### Nmap

```bash
nmap -sC -sV -oA nmap/initial 10.10.10.x
```

```
# Paste nmap output here
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH x.x
80/tcp open  http    Apache x.x
```

### Web Enumeration

```bash
# Directory brute force
ffuf -w /usr/share/wordlists/seclists/Discovery/Web-Content/common.txt -u http://10.10.10.x/FUZZ

# Subdomain enumeration
ffuf -w /usr/share/wordlists/seclists/Discovery/DNS/subdomains-top1million-5000.txt -H "Host: FUZZ.domain.htb" -u http://10.10.10.x
```

### Additional Enumeration

```bash
# Add any other enumeration steps here (SMB, FTP, etc.)
```

---

## Foothold

### Vulnerability Discovery

Describe what you found and how. What vulnerability or misconfiguration did you identify?

```bash
# Commands used to identify/exploit the vulnerability
```

### Exploitation

Step by step exploitation. Be specific about what you did and why.

```bash
# Exploit commands
```

```
# Relevant output
```

---

## Lateral Movement

> Skip this section if not applicable

Describe any lateral movement between users or services.

```bash
# Commands used
```

---

## Privilege Escalation

### Enumeration

```bash
# Local enumeration commands
sudo -l
find / -perm -4000 2>/dev/null
cat /etc/crontab
```

### Exploitation

Describe the privilege escalation vector and how you exploited it.

```bash
# Privesc commands
```

---

## Flags

```bash
# User flag
cat /home/<user>/user.txt

# Root flag
cat /root/root.txt
```

| Flag | Hash |
|------|------|
| User | `XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX` |
| Root | `XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX` |

---

## Lessons Learned

- What did you learn from this box?
- What would you do differently?
- Any new tools or techniques discovered?

---

## References

- [HTB Machine Page](https://app.hackthebox.com/machines/)
- [Relevant CVE](https://cve.mitre.org)
- [Tool/Technique Used](https://example.com)
