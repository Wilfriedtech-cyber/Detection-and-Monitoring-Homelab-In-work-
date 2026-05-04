# 🛡️ Detection & Monitoring Home Lab

## 📘 Introduction
Welcome to my first **Detection and Monitoring Home Lab**.

This lab was built to strengthen my blue-team and SOC skills by simulating real-world attacks against vulnerable systems and analyzing the resulting telemetry inside **Splunk SIEM**.

---

## 🎯 Goals
The primary goals of this lab are:

- Develop **detection engineering skills** using Splunk  
- Simulate attacks against **vulnerable services**
- Centralize and analyze logs from multiple security controls
- Understand how logs flow **end-to-end**, from endpoint/network → SIEM
- Practice writing and tuning **detection rules**

---

## 🤔 Why This Lab?
After passing **BTL1**, I wanted to go beyond theory and labs by:

- Building something **from scratch**
- Understanding what actually happens **behind the scenes**
- Learning how logs are generated, forwarded, parsed, and correlated in Splunk

While researching SOC lab ideas, I found inspiration from:
- **Nakkouch Tarek** *(https://medium.com/@nakkouchtarek/from-zero-to-soc-homelab-my-journey-to-defense-in-depth-and-full-security-automation-cc07373b8b6d)*
- **Day Johnson** *(https://blog.cyberwoxacademy.com/post/building-a-cybersecurity-homelab)*

Rather than cloning an existing lab, I wanted to be **creative** and design my own architecture.  
This is a **small foundational network**, which I plan to **expand over time**.

---

## 🧠 Skills Gained
- Splunk searches & SPL
- Log correlation
- Sysmon log investigation
- Network security monitoring
- IDS/IPS alert analysis
- Detection engineering fundamentals
- SIEM log ingestion & parsing

---

## 🧩 Network Topology

<img width="902" height="673" alt="image" src="https://github.com/user-attachments/assets/f52a1048-8ae7-48d8-9de9-a32881951f11" />



> *Diagram overview of the lab environment and log flow.*

---

## 🧪 Lab Architecture Explained

### 1️⃣ Public-Facing Services (Attack Surface)
- A **private IP** is assigned to **PFsense** acting as the network gateway.
- Open ports:
  - **Port 22** → SSH (Cowrie honeypot)
  - **Port 80** → DVWA (Web server)
- Caldera agent Installed on Domain controller and windows client to simulate **MITRE ATT&CK TTPS**

---

### 2️⃣ Network Security & Traffic Monitoring
- **pfSense** is used as:
  - Router
  - Firewall
  - IDS/IPS
- **Suricata** is enabled on pfSense
- All firewall and IDS/IPS logs are forwarded to **Splunk**

---

### 3️⃣Endpoint Monitoring
- **Sysmon** is installed on:
  - Domain Controller
  - Client machine
- Provides detailed visibility into:
  - Process creation
  - Network connections
  - File modifications
- Logs are forwarded to **Splunk** for detection and investigation

---

## 🔭 What’s Next?
This lab is a living project.

Upcoming improvements will include:
- More attack simulations( Mittre Caldera )
- Custom detection rules
- Additional data sources
- Threat hunting scenarios

---

🚀 **Stay tuned — I’ll be documenting how this lab was built step by step!**
