# 🛠️ Building a Vulnerable Machine (DVWA + ModSecurity IDS + Cowrie)

This section explains how to build a vulnerable lab environment including:

- DVWA (Damn Vulnerable Web Application)
- ModSecurity (running in IDS / Detection mode)
- OWASP Core Rule Set (CRS)
- Cowrie SSH Honeypot

---

## 🎯 Purpose

- 🔍 Web security testing
- 🧪 WAF/IDS analysis
- 🎯 Simulating attacks (SQLi, XSS, scans)
- 📊 Monitoring logs and attacker behavior

---

## ⚙️ Requirements

- Ubuntu (VM recommended)
- Apache2
- PHP + MySQL/MariaDB
- Git
- Kali Linux (attacker machine)

---

# Install DVWA

I followed this video for the DVWA installation, as it covers every step in a straightforward manner:

https://www.youtube.com/watch?v=5PBZJg6-Gd4&t=14s

> **Note:** I recommend not changing the default username and password of the DVWA PHP configuration.

<img width="1289" height="835" alt="image" src="https://github.com/user-attachments/assets/afa24a77-979e-4c2f-bc9a-c842f00952fc" />
<img width="1548" height="924" alt="image" src="https://github.com/user-attachments/assets/8072d2c5-c037-484c-9f70-26bb6f0bf5a8" />
<img width="1293" height="839" alt="image" src="https://github.com/user-attachments/assets/b53a0e5d-ff83-4165-827d-6d095276c1a6" />

---

# Install ModSecurity

## 1. Update Your System
```bash
sudo apt update
sudo apt upgrade -y
```

## 2. Install Apache
```bash
sudo apt install apache2 -y
sudo systemctl enable apache2
sudo systemctl start apache2
systemctl status apache2
```

Open a browser and visit:
```
http://your_server_ip
```
You should see the Apache default page.

## 3. Install ModSecurity
```bash
sudo apt install libapache2-mod-security2 -y
```

<img width="1294" height="821" alt="image" src="https://github.com/user-attachments/assets/dca37592-ced2-4742-833e-2b9afe9751e3" />
<img width="1290" height="835" alt="image" src="https://github.com/user-attachments/assets/deaa7393-08f4-4112-bcfd-78c53d8c0828" />

Verify the installation:
```bash
apachectl -M | grep security
```

Expected output:
```
security2_module (shared)
```

## 4. Enable the ModSecurity Module
```bash
sudo a2enmod security2
sudo systemctl restart apache2
```

## 5. Enable the ModSecurity Engine
```bash
cd /etc/modsecurity
sudo cp modsecurity.conf-recommended modsecurity.conf
sudo nano modsecurity.conf
```

Locate the following line:
```
SecRuleEngine DetectionOnly
```

The available modes are:

| Mode | Behavior |
|------|----------|
| Off | Disabled |
| DetectionOnly | IDS (logs attacks) |
| On | IPS/WAF (blocks attacks) |

For IDS mode, leave it as:
```
SecRuleEngine DetectionOnly
```

Save and exit.

<img width="1293" height="841" alt="image" src="https://github.com/user-attachments/assets/f30528cf-3c81-40b7-98ba-22cc50f16ec9" />

## 6. Install the OWASP Core Rule Set (CRS)

The OWASP CRS provides detection rules for:
- SQL injection
- XSS
- Command injection
- LFI/RFI
- Web shell attempts
- Scanners

```bash
sudo apt install git -y
cd /usr/share
sudo git clone https://github.com/coreruleset/coreruleset.git
sudo mv coreruleset owasp-crs
cd /usr/share/owasp-crs
sudo cp crs-setup.conf.example crs-setup.conf
```

## 7. Configure Apache to Use CRS
```bash
sudo nano /etc/apache2/mods-enabled/security2.conf
```

Add the following lines at the bottom:
```
IncludeOptional /usr/share/owasp-crs/crs-setup.conf
IncludeOptional /usr/share/owasp-crs/rules/*.conf
```

Save and exit.

## 8. Restart Apache
```bash
sudo systemctl restart apache2
```

<img width="1291" height="833" alt="image" src="https://github.com/user-attachments/assets/502bf2fb-6b6d-43ad-887a-7da19981e552" />

## 9. Verify ModSecurity is Running
```bash
apachectl -M | grep security
sudo tail -f /var/log/apache2/modsec_audit.log
```

<img width="1221" height="370" alt="image" src="https://github.com/user-attachments/assets/f929a94b-c92d-4db2-8d65-2a11b545454c" />

## 10. Enable Detailed Logging
```bash
sudo nano /etc/modsecurity/modsecurity.conf
```

Ensure the following lines are present:
```
SecAuditEngine On
SecAuditLog /var/log/apache2/modsec_audit.log
SecAuditLogParts ABIJDEFHZ
```

## 11. Useful Commands

Restart Apache:
```bash
sudo systemctl restart apache2
```

Check ModSecurity logs:
```bash
sudo tail -f /var/log/apache2/modsec_audit.log
```

Check Apache error logs:
```bash
sudo tail -f /var/log/apache2/error.log
```

---

<img width="1297" height="832" alt="image" src="https://github.com/user-attachments/assets/a1a2f68e-0f77-407d-af8e-ec68b05f845e" />

---

# 🍯 Cowrie SSH Honeypot Setup

Cowrie is used to capture and log attacker activity over SSH.

## 1. Installation Reference

I followed this video for the Cowrie installation:

https://www.youtube.com/watch?v=-ufsdzLr5Oc

## 2. Start Cowrie
```bash
cd cowrie
bin/cowrie start
```

## 3. Monitor Logs
```bash
tail -f /var/log/cowrie/cowrie.log
```

## 4. Observing Attacks

From your attacker machine (Kali), run:
```bash
nmap -A <target-ip>
```

You should see:
- Open SSH port
- Activity captured in Cowrie logs

---

## 📊 Useful Commands

**Apache:**
```bash
sudo systemctl restart apache2
sudo systemctl status apache2
```

**ModSecurity Logs:**
```bash
sudo tail -f /var/log/apache2/modsec_audit.log
```

**Apache Logs:**
```bash
sudo tail -f /var/log/apache2/error.log
```

**Cowrie Logs:**
```bash
tail -f /var/log/cowrie/cowrie.log
```

---

> ✔ Your vulnerable machine is now fully set up. Congratulations!

---

## TLDR

> I highly recommend using the default configuration throughout the setup process. Once everything is working, you can make any modifications you'd like, such as changing usernames, passwords, or other settings.
