# SPLUNK CONFIGURATION



# 1️⃣ Download Splunk Enterprise

Open a browser on Ubuntu and go to:

https://www.splunk.com/en_us/download/splunk-enterprise.html
Make sure to create an account

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

Open a **terminal**.

Navigate to the Downloads folder:

```
cd ~/Downloads
```

Install Splunk using `dpkg`:

```
sudo dpkg-i splunk*.deb
```

<img width="1289" height="824" alt="image" src="https://github.com/user-attachments/assets/4739dad8-55a6-4981-bfe0-7b7eb8aad7b4" />


If dependencies are missing run:

```
sudo apt--fix-broken install
```

<img width="1298" height="843" alt="image" src="https://github.com/user-attachments/assets/22cf7765-2ef9-40f9-8283-5ac6e284c9a7" />


---

# 3️⃣ Start Splunk for the First Time

Splunk installs in:

```
/opt/splunk
```

Start Splunk:

```
sudo /opt/splunk/bin/splunkstart
```

You will see the **license agreement**.

Type:

```
y
```

Then create an **admin username and password**.

Example:

```
username: admin
password: strongpassword
```

<img width="1315" height="839" alt="image" src="https://github.com/user-attachments/assets/f4494da7-70f9-4ac7-b476-9af5a1e97867" />


---

# 4️⃣ Enable Splunk to Start Automatically

Run:

```
sudo /opt/splunk/bin/splunk enable boot-start
```


<img width="1298" height="843" alt="image" src="https://github.com/user-attachments/assets/d27b390b-e2d6-41f3-b298-63943fb5b033" />


This ensures Splunk starts when Ubuntu boots.

---

# 5️⃣ Open the Splunk Web Interface

On Ubuntu, open a browser and go to:

```
http://localhost:8000
```

<img width="1296" height="840" alt="image" src="https://github.com/user-attachments/assets/00c6c479-0f90-4f0f-994e-ad6ee9ae4e98" />


If accessing from another machine:

```
http://UBUNTU_IP:8000
```

Example:

```
http://192.168.1.50:8000
```

Login using the admin credentials you created.

---

# 6️⃣ Configure the Splunk Receiving Port

To receive logs from other machines (like Windows):

1. Go to **Settings**
2. Click **Forwarding and receiving**
3. Click **Configure receiving**
4. Click **New Receiving Port**

<img width="1291" height="840" alt="image" src="https://github.com/user-attachments/assets/e39fb8a4-b1a9-452b-b2eb-e8f7a2b7a2a1" />

<img width="1281" height="842" alt="image" src="https://github.com/user-attachments/assets/70fbba09-40b9-421b-8ad8-ca4afafb0a91" />

<img width="1303" height="833" alt="image" src="https://github.com/user-attachments/assets/d01689ba-4989-48d0-b414-24da3095dfe3" />


Set port:

```
9997
```

Save.

This allows **forwarders to send logs to Splunk**.


My splunk instance should be on: 
http://loclahost:8000/ or the domain name in that screenshot.

It will receive logs on port 8989
