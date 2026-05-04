# Splunk Configuration

---

# 1️⃣ Download Splunk Enterprise

Open a browser on Ubuntu and go to:

https://www.splunk.com/en_us/download/splunk-enterprise.html

> Make sure to create an account first.

Choose:
```
Linux (.deb) – 64 bit
```

You will download a file like:
```
splunk-9.x.x-linux-amd64.deb
```

---

# 2️⃣ Install Splunk on Ubuntu

Open a **terminal** and navigate to the Downloads folder:
```bash
cd ~/Downloads
```

Install Splunk using `dpkg`:
```bash
sudo dpkg -i splunk*.deb
```

<img width="1289" height="824" alt="image" src="https://github.com/user-attachments/assets/4739dad8-55a6-4981-bfe0-7b7eb8aad7b4" />

If any dependencies are missing, run:
```bash
sudo apt --fix-broken install
```

<img width="1298" height="843" alt="image" src="https://github.com/user-attachments/assets/22cf7765-2ef9-40f9-8283-5ac6e284c9a7" />

---

# 3️⃣ Start Splunk for the First Time

Splunk installs to:
```
/opt/splunk
```

Start Splunk:
```bash
sudo /opt/splunk/bin/splunk start
```

You will be prompted to accept the **license agreement**. Type:
```
y
```

Then create an **admin username and password**:
```
Username: admin
Password: strongpassword
```

<img width="1315" height="839" alt="image" src="https://github.com/user-attachments/assets/f4494da7-70f9-4ac7-b476-9af5a1e97867" />

---

# 4️⃣ Enable Splunk to Start Automatically

Run the following command to ensure Splunk starts on boot:
```bash
sudo /opt/splunk/bin/splunk enable boot-start
```

<img width="1298" height="843" alt="image" src="https://github.com/user-attachments/assets/d27b390b-e2d6-41f3-b298-63943fb5b033" />

---

# 5️⃣ Open the Splunk Web Interface

On Ubuntu, open a browser and go to:
```
http://localhost:8000
```

<img width="1296" height="840" alt="image" src="https://github.com/user-attachments/assets/00c6c479-0f90-4f0f-994e-ad6ee9ae4e98" />

If accessing from another machine on the network:
```
http://<UBUNTU_IP>:8000
```

Example:
```
http://192.168.1.50:8000
```

Log in using the admin credentials you created.

---

# 6️⃣ Configure the Splunk Receiving Port

To receive logs from other machines such as Windows forwarders:

1. Go to **Settings**
2. Click **Forwarding and Receiving**
3. Click **Configure Receiving**
4. Click **New Receiving Port**

<img width="1291" height="840" alt="image" src="https://github.com/user-attachments/assets/e39fb8a4-b1a9-452b-b2eb-e8f7a2b7a2a1" />
<img width="1281" height="842" alt="image" src="https://github.com/user-attachments/assets/70fbba09-40b9-421b-8ad8-ca4afafb0a91" />
<img width="1303" height="833" alt="image" src="https://github.com/user-attachments/assets/d01689ba-4989-48d0-b414-24da3095dfe3" />

Set the receiving port:
```
8989
```

> You can use any port number you prefer. I chose **8989** for this setup.

Click **Save**.

This allows **Splunk Universal Forwarders** to send logs to your Splunk instance.

> **Note:** My Splunk instance is accessible at `http://localhost:8000` or via the domain name shown in the screenshot above. It receives forwarded logs on port **8989**.
