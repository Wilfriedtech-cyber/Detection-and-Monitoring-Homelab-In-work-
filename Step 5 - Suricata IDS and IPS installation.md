# Suricata IDS/IPS Configuration on pfSense

## Installation Reference

I followed this video for the Suricata installation on pfSense:

https://www.youtube.com/watch?v=LaB6-Klnh7w

---

## Accessing Suricata

Once installed, navigate to **Services** in the pfSense web UI — you should see **Suricata** listed underneath it.

<img width="1283" height="841" alt="image" src="https://github.com/user-attachments/assets/2630fc34-e9d5-4ebc-b83a-270e3cb45c34" />

---

## Managing Rules

The **SID Mgmt** tab is where you can create and manage detection rules.

<img width="1294" height="803" alt="image" src="https://github.com/user-attachments/assets/3f22a575-260f-481d-a855-0a53b5ebdee9" />

> **Note:** At this stage, Kali Linux is able to reach the pfSense interface because all firewall rules are currently open for initial configuration purposes. This will be secured once everything is verified to be communicating correctly.

From here you can add any rules to detect and log network activity across your interfaces.
