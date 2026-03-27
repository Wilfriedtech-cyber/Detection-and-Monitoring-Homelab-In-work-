# 🛠️ Building a Vulnerable Machine (DVWA + ModSecurity IDS + Cowrie)

This section explains how to build a vulnerable lab environment including:

- DVWA (Damn Vulnerable Web Application)
- ModSecurity (running in IDS / Detection mode)
- OWASP Core Rule Set (CRS)
- Cowrie SSH Honeypot

---

## 🎯 Purpose

This lab is designed for:

- 🔍 Web security testing
- 🧪 WAF/IDS analysis
- 🎯 Simulating attacks (SQLi, XSS, scans)
- 📊 Monitoring logs and attacker behavior


## ⚙️ Requirements

- Ubuntu (VM recommended)
- Apache2
- PHP + MySQL/MariaDB
- Git
- Kali Linux (attacker machine)

---

# 🔓 DVWA Setup

## 1. Start Apache

```bash
sudo systemctl start apache2
sudo systemctl status apache2

---
## 2. S
