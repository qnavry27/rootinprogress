---
title: "21 - File Transfer Protocol"
date: 2026-03-10
draft: false
description: "A practical cheatsheet for FTP covering common commands and use cases."
tags: ["ftp", "cheatsheet"]
categories: ["Cheatsheets"]
showToc: true
TocOpen: true
alt: "FTP Cheatsheet"
---

## Overview

File Transfer Protocol is a standard network protocol used to transfer filees betwee na client and server over TCP/IP.
It operates on port 21 (control) and port 20 (data)

Category: Enumeration / File Transfer / Post-Exploitation
Default Port: 21 (control), 20 (data)
Protocol: TCP

---

## Checklist

- [ ] Anonymous login enabled?
- [ ] Writable directories?
- [ ] Interesting files (credentials, configs, backups)?
- [ ] Banner grabbing for version info
- [ ] Known CVEs for the FTP version?
- [ ] Brute force credentials

## Enumeration
 
### Nmap
 
```bash
# Basic FTP scan
nmap -sC -sV -p 21 <target>
 
# FTP specific scripts
nmap --script ftp-anon,ftp-bounce,ftp-brute,ftp-syst -p 21 <target>
 
# Check for anonymous login
nmap --script ftp-anon -p 21 <target>
```
 
### Banner Grabbing
 
```bash
# Netcat
nc -nv <target> 21
 
# Telnet
telnet <target> 21
```
 
---
 
## Authentication
 
### Anonymous Login
 
```bash
ftp <target>
# Username: anonymous
# Password: anonymous (or leave blank)
 
# One-liner
ftp -n <target> <<EOF
quote USER anonymous
quote PASS anonymous
EOF
```
 
### Standard Login
 
```bash
ftp <target>
# Username: <user>
# Password: <password>
```
 
---
## File Transfers
 
### Download Files
 
```bash
# Single file
ftp> get filename.txt
 
# All files in directory
ftp> mget *
 
# Download recursively (using wget)
wget -m ftp://anonymous:anonymous@<target>
 
# Download recursively (using curl)
curl -s ftp://<target>/ --user anonymous:anonymous
```
 
### Upload Files
 
```bash
# Single file
ftp> put shell.php
 
# Always switch to binary mode for non-text files
ftp> binary
ftp> put shell.php
```
 
---
 
## Passive vs Active Mode
 
```bash
# Enable passive mode (use when behind NAT/firewall)
ftp> passive
 
# Force passive mode from command line
ftp -p <target>
```
 
---
 
## Brute Force
 
```bash
# Hydra
hydra -l <user> -P /usr/share/wordlists/rockyou.txt ftp://<target>
hydra -L users.txt -P passwords.txt ftp://<target> -t 4
 
# Medusa
medusa -h <target> -u <user> -P /usr/share/wordlists/rockyou.txt -M ftp
 
# Nmap brute
nmap --script ftp-brute -p 21 <target>
```
 
---
 
## Post-Exploitation / Interesting Files
 
```bash
# Look for these files
ftp> ls -la
 
# Common interesting locations
/var/www/html          # Web root
/etc/passwd            # User list
/home/<user>/.ssh      # SSH keys
/backup                # Backup files
/var/backups           # System backups
 
# Download everything for offline analysis
wget -m ftp://user:password@<target>
```
 
---
 
## Config Files (Server-Side)
 
```bash
# vsftpd
/etc/vsftpd.conf
/etc/vsftpd/vsftpd.conf
 
# ProFTPD
/etc/proftpd/proftpd.conf
 
# Pure-FTPd
/etc/pure-ftpd/pure-ftpd.conf
```
 
---
 
## FTP Bounce Attack
 
```bash
# Check if vulnerable
nmap --script ftp-bounce -p 21 <target>
 
# Use FTP server to port scan internal network
nmap -b anonymous:anonymous@<target> <internal-target>
```
 
---
 
## Tips & Tricks
 
- Always try **anonymous login** first — surprisingly common on CTFs and misconfigured servers
- Switch to **binary mode** before transferring executables or archives to avoid corruption
- Use `mget *` to grab everything at once for offline analysis
- Check for **writable directories** — if you can upload a webshell and the FTP root overlaps with the web root, you have RCE
- `wget -m` is the fastest way to mirror an entire FTP share locally
