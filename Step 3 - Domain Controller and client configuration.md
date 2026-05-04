# Active Directory & Adding a Client to the Domain Controller

---

# 1️⃣ Install Active Directory Domain Services on the Server

> **Note:** Always use the same password throughout the setup. My domain is **lab.local**. Remember to change the preferred DNS on the client to the server's IP address.

## Step 1 — Open Server Manager
1. Log in to your **Windows Server**
2. Open **Server Manager** (it opens automatically on login)

## Step 2 — Add Roles and Features
1. Click **Manage**
2. Click **Add Roles and Features**

## Step 3 — Installation Type
Select:

✔ **Role-based or feature-based installation**

<img width="1032" height="798" alt="image" src="https://github.com/user-attachments/assets/127e0c6a-f695-4c62-8431-dd23ac8be496" />

Click **Next**

## Step 4 — Select Server
Choose your server from the list → Click **Next**

## Step 5 — Select Roles
Check:

✔ **Active Directory Domain Services**

A popup will appear.

<img width="1035" height="800" alt="image" src="https://github.com/user-attachments/assets/158d3e13-e323-4eda-b443-ece9a7c42ed5" />

Click:

✔ **Add Features**

Then click **Next**

<img width="1036" height="804" alt="image" src="https://github.com/user-attachments/assets/db93bdcf-8706-4a26-a37b-141d1b11d54a" />

## Step 6 — Install
Click **Next** until you reach the **Install** screen, then click:

✔ **Install**

Wait for the installation to complete.

<img width="1034" height="804" alt="image" src="https://github.com/user-attachments/assets/2593780c-d9f3-4d65-952c-3e9f2bfa8ade" />

---

# 2️⃣ Promote the Server to a Domain Controller

Once the installation is complete:

## Step 1
Click the **flag notification icon** in Server Manager and select:

**Promote this server to a domain controller**

## Step 2 — Deployment Configuration

<img width="1033" height="814" alt="image" src="https://github.com/user-attachments/assets/10ddc261-4007-4c58-b791-8f507c46080e" />

Select:

✔ **Add a new forest**

<img width="1041" height="806" alt="image" src="https://github.com/user-attachments/assets/780783c0-7c10-41e6-8724-bd0e352a8d5f" />

Set the root domain name:

```
lab.local
```

<img width="1036" height="804" alt="image" src="https://github.com/user-attachments/assets/100e0153-0a54-4dd9-996e-48ad9a5a35fb" />

Click **Next**

## Step 3 — Domain Controller Options
Set:

✔ Forest functional level

✔ Domain functional level

Enter a **DSRM password** and keep it safe.

Click **Next**

## Step 4 — DNS Options
Ignore the warning and click **Next**

## Step 5 — Additional Options
Confirm your domain name and click **Next**

## Step 6 — Paths
Leave the default paths as they are:
```
NTDS
SYSVOL
Logs
```

Click **Next**

## Step 7 — Review and Install
Click **Install**

The server will **restart automatically**. After the reboot, the server is now a fully configured **Domain Controller**.

---

# 3️⃣ Configure DNS on the Client

Before joining the domain, the client machine must point to the **Domain Controller as its DNS server**.

On the **Windows client**:

1. Open **Control Panel**
2. Go to **Network and Internet**
3. Click **Network and Sharing Center**
4. Click **Change adapter settings**
5. Right-click your network adapter → **Properties**
6. Select **Internet Protocol Version 4 (IPv4)**
7. Click **Properties**

Set the DNS server to the **Domain Controller's IP address**:

```
Preferred DNS: 192.168.x.x   (your Domain Controller IP)
```

Click **OK**

---

# 4️⃣ Join the Client Computer to the Domain

On the **Windows client**:

## Step 1
Right-click **This PC** → Click **Properties**

## Step 2
Click **Advanced system settings**

<img width="1044" height="813" alt="image" src="https://github.com/user-attachments/assets/85b29d9b-71ee-4eb9-b485-0ff568dc2b05" />

Go to the **Computer Name** tab and click **Change**

## Step 3 — Join the Domain
Select:

✔ **Domain**

Enter your domain name:
```
lab.local
```

Click **OK**

<img width="1036" height="809" alt="image" src="https://github.com/user-attachments/assets/6ec2f41d-9f0e-4331-af40-2ecd5e147753" />

## Step 4 — Enter Credentials
When prompted, enter your domain administrator credentials:
```
Username: Administrator
Password: ********
```

## Step 5
You should see:

✅ **Welcome to the domain**

Restart the computer.

<img width="1048" height="818" alt="image" src="https://github.com/user-attachments/assets/56e354c0-dc58-44ca-bdda-bd352583b3e9" />

---

# 5️⃣ Log into the Domain

After the restart, at the login screen click **Other user** and log in using:

```
lab\administrator
```
or
```
administrator@lab.local
```

---

# 6️⃣ Verify the Client Appears in Active Directory

On the **Domain Controller**, open:

```
Active Directory Users and Computers
```

Navigate to **Computers** — you should see the **client machine listed**.

<img width="1031" height="803" alt="image" src="https://github.com/user-attachments/assets/ea1e76e0-b6f4-40ff-b7f5-3458fd551665" />
