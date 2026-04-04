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

## Step1 Start Apache

  bash
  sudo systemctl start apache2
  sudo systemctl status apache2

2. Access DVWA

Open in browser:

http://localhost/DVWA

Default credentials:

username: admin
password: password
3. Configure Database
cd /var/www/html/DVWA/config
sudo nano config.inc.php

Example configuration:

$_DVWA['db_server'] = '127.0.0.1';
$_DVWA['db_database'] = 'dvwa';
$_DVWA['db_user'] = 'dvwa';
$_DVWA['db_password'] = 'p@ssw0rd';

Then initialize:

http://localhost/DVWA/setup.php

Click Create / Reset Database

🛡️ ModSecurity (IDS Mode)
1. Update System
sudo apt update
sudo apt upgrade -y
2. Install Apache (if not installed)
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2
3. Install ModSecurity
sudo apt install libapache2-mod-security2 -y

Verify installation:

apachectl -M | grep security

Expected output:

security2_module (shared)
4. Enable ModSecurity
sudo a2enmod security2
sudo systemctl restart apache2
5. Configure IDS Mode
cd /etc/modsecurity
sudo cp modsecurity.conf-recommended modsecurity.conf
sudo nano modsecurity.conf

Find:

SecRuleEngine DetectionOnly
Modes
Mode	Description
Off	Disabled
DetectionOnly	IDS (logs only)
On	Blocking (WAF mode)

Keep:

SecRuleEngine DetectionOnly
📦 Install OWASP CRS
sudo apt install git -y
cd /usr/share
sudo git clone https://github.com/coreruleset/coreruleset.git
sudo mv coreruleset owasp-crs
cd owasp-crs
sudo cp crs-setup.conf.example crs-setup.conf
Configure Apache to Use CRS
sudo nano /etc/apache2/mods-enabled/security2.conf

Add:

IncludeOptional /usr/share/owasp-crs/crs-setup.conf
IncludeOptional /usr/share/owasp-crs/rules/*.conf

Restart Apache:

sudo systemctl restart apache2
🔍 Verify ModSecurity

Check module:

apachectl -M | grep security

Monitor logs:

sudo tail -f /var/log/apache2/modsec_audit.log
🧪 Test Detection
XSS Test
curl "http://localhost/?test=<script>alert(1)</script>"
SQL Injection Test
curl "http://localhost/index.php?id=1' OR '1'='1"

Check logs:

sudo tail -f /var/log/apache2/modsec_audit.log

You should see detected attacks logged.

🧾 Enable Detailed Logging
sudo nano /etc/modsecurity/modsecurity.conf

Ensure:

SecAuditEngine On
SecAuditLog /var/log/apache2/modsec_audit.log
SecAuditLogParts ABIJDEFHZ
🍯 Cowrie SSH Honeypot Setup

Cowrie is used to capture attacker activity on SSH.

1. Installation Reference

Follow:

https://www.youtube.com/watch?v=-ufsdzLr5Oc

2. Start Cowrie
cd cowrie
bin/cowrie start
3. Monitor Logs
tail -f /var/log/cowrie/cowrie.log
4. Observing Attacks

From attacker machine (Kali):

nmap -A <target-ip>

You should see:

Open SSH port
Activity captured in Cowrie logs
📊 Useful Commands
Apache
sudo systemctl restart apache2
sudo systemctl status apache2
ModSecurity Logs
sudo tail -f /var/log/apache2/modsec_audit.log
Apache Logs
sudo tail -f /var/log/apache2/error.log
Cowrie Logs
tail -f /var/log/cowrie/cowrie.log

# TLDR


I would highly recommend to use the default configuration and once you finish with everything you can make any modification you would like (such as changing password, username etc ...)
