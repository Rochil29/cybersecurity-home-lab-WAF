# Web Application Firewall Home Lab (SafeLine WAF)

## Overview
A complete cybersecurity home lab built using VirtualBox, 
Kali Linux, Ubuntu Server, DVWA, and SafeLine WAF.
The lab demonstrates real-world web application attacks 
and how a WAF detects and blocks them.

Based on the guide by Royden Rebello (The Social Dork)
Reference video: https://youtu.be/N0dEC1nuWCQ

---

## Lab Architecture

| Component        | Details                        |
|-----------------|-------------------------------|
| Kali Linux      | 192.168.1.3 (Attacker)        |
| Ubuntu Server   | 192.168.1.5 (Target + WAF)   |
| DVWA            | Port 8080 (Apache backend)    |
| SafeLine WAF    | Port 9443 (Admin), 443 (HTTPS)|
| Domain          | dvwa.local                    |

---

## Tools Used
- VirtualBox
- Kali Linux
- Ubuntu Server 22.04 LTS
- DVWA (Damn Vulnerable Web Application)
- SafeLine WAF (v9.3.6)
- Apache2, PHP 8.5, MySQL 8.4
- OpenSSL (self-signed certificate)
- Docker (SafeLine runs on Docker)

---

## What Was Set Up
- Ubuntu Server with LAMP stack
- DVWA installed and configured on port 8080
- Self-signed SSL certificate
- SafeLine WAF as HTTPS reverse proxy on port 443
- Local DNS using /etc/hosts (dvwa.local)
- Kali Linux SSH'd into Ubuntu for management

---

## Attacks Demonstrated

### With WAF Protection ON (blocked):
- SQL Injection — Access Forbidden
- XSS (Reflected) — Access Forbidden
- Command Injection — Access Forbidden
- File Upload (PHP shell) — Access Forbidden
- File Inclusion (/etc/passwd) — Access Forbidden

### With WAF Protection OFF (exploited):
- SQL Injection — dumped all users from database
- XSS — browser alert popup executed
- Command Injection — ran whoami and cat /etc/passwd
- File Upload — PHP web shell uploaded successfully
- File Inclusion — /etc/passwd contents exposed

---

## Key Problems Solved
1. DVWA 500 error — MySQL user misconfigured + 
   PHP allow_url_include was Off
2. Browser bypassing WAF — fixed with Apache 
   ServerName + UseCanonicalName directives
3. Copy/paste between VMs — used SCP to transfer 
   SSL certificate files
4. Working in wrong directory — always run cd ~ first

---

## Documentation
Full lab documentation with all steps, commands,
problems and solutions is in:
docs/SafeLine_WAF_Lab_Documentation.docx

## Screenshots
All attack demonstrations with and without WAF 
protection are in the screenshots/ folder

---

## Disclaimer
This lab is for educational purposes only.
All testing was done in an isolated home lab environment.
Never use these techniques on systems you don't own.
