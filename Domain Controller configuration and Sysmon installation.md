# ACTIVE DIRECTORY AND CLIENT ADDING TO THE DOMAIN CONTROLLER

# 1️⃣ Install Active Directory Domain Services on the Server

### REMEMBER ALWAYS SAME PASSWORD BUT MY DOMAIN IS LAB and 
change DNS (preferred dns) ip on client to the server ip
Step 1 — Open Server Manager

1. Log in to your **Windows Server**.
2. Open **Server Manager** (opens automatically on login).

### Step 2 — Add Roles and Features

1. Click **Manage**
2. Click **Add Roles and Features**

### Step 3 — Installation Type

Select:

✔ **Role-based or feature-based installation**

<img width="1032" height="798" alt="image" src="https://github.com/user-attachments/assets/127e0c6a-f695-4c62-8431-dd23ac8be496" />


Click **Next**

### Step 4 — Select Server

Choose your server from the list → **Next**

### Step 5 — Select Roles

Check:

✔ **Active Directory Domain Services**

A popup appears.

<img width="1035" height="800" alt="image" src="https://github.com/user-attachments/assets/158d3e13-e323-4eda-b443-ece9a7c42ed5" />


Click:

✔ **Add Features**

Click **Next**

<img width="1036" height="804" alt="image" src="https://github.com/user-attachments/assets/db93bdcf-8706-4a26-a37b-141d1b11d54a" />


### Step 6 — Continue

Click **Next** until you reach **Install**

Click:

✔ **Install**

Wait for installation to finish.

<img width="1034" height="804" alt="image" src="https://github.com/user-attachments/assets/2593780c-d9f3-4d65-952c-3e9f2bfa8ade" />


---

# 2️⃣ Promote Server to Domain Controller

After installation finishes:

### Step 1

Click the **flag notification icon** in Server Manager.

Click:

**Promote this server to a domain controller**

### Step 2 — Deployment Configuration

<img width="1033" height="814" alt="image" src="https://github.com/user-attachments/assets/10ddc261-4007-4c58-b791-8f507c46080e" />

Select:

✔ **Add a new forest**

<img width="1041" height="806" alt="image" src="https://github.com/user-attachments/assets/780783c0-7c10-41e6-8724-bd0e352a8d5f" />


Root domain name example:

<img width="1036" height="804" alt="image" src="https://github.com/user-attachments/assets/100e0135-0a54-4dd9-996e-48ad9a5a35fb" />

```
lab.local
```

Click **Next**

---

### Step 3 — Domain Controller Options

Set:

✔ Forest functional level

✔ Domain functional level

Enter a **DSRM password** (important).

Click **Next**

---

### Step 4 — DNS Options

Ignore the warning and click **Next**

---

### Step 5 — Additional Options

Confirm your domain name.

Click **Next**

---

### Step 6 — Paths

Leave default paths:

```
NTDS
SYSVOL
Logs
```

Click **Next**

---

### Step 7 — Review

Click **Install**

The server will **restart automatically**.

After reboot, the server is now a **Domain Controller**.

---

# 3️⃣ Configure DNS on the Client

Before joining the domain, the client must use the **Domain Controller as DNS**.

On the **Windows client**:

1. Open **Control Panel**
2. Go to:

```
Network and Internet
```

1. Click:

```
Network and Sharing Center
```

1. Click:

```
Change adapter settings
```

1. Right-click your network adapter → **Properties**
2. Select:

```
Internet Protocol Version 4 (IPv4)
```

1. Click **Properties**

Set DNS server to the **Domain Controller IP**.

Example:

```
Preferred DNS: 192.168.1.10   (Domain Controller IP)
```

Click **OK**

---

# 4️⃣ Join the Client Computer to the Domain

On the **Windows client**:

### Step 1

Right-click:

```
This PC
```

Click:

```
Properties
```

---

### Step 2

Click:

```
Advanced system settings
```

<img width="1044" height="813" alt="image" src="https://github.com/user-attachments/assets/85b29d9b-71ee-4eb9-b485-0ff568dc2b05" />


Then click:

```
Computer Name tab
```

Click:

```
Change
```

---

### Step 3 — Join Domain

Select:

✔ **Domain**

Enter your domain name:

```
lab.local
```

Click **OK**

<img width="1036" height="809" alt="image" src="https://github.com/user-attachments/assets/6ec2f41d-9f0e-4331-af40-2ecd5e147753" />

---

### Step 4 — Enter Credentials

Enter:

```
Domain Administrator
```

Example:

```
Username: Administrator
Password: ********
```

---

### Step 5

You should see:

✅ **Welcome to the domain**

Restart the computer.

<img width="1048" height="818" alt="image" src="https://github.com/user-attachments/assets/56e354c0-dc58-44ca-bdda-bd352583b3e9" />

---

# 5️⃣ Log into the Domain

After restart:

At the login screen click:

```
Other user
```

Login using:

```
lab\administrator
```

or

```
administrator@lab.local
```

---

# 6️⃣ Verify Client Appears in Active Directory

On the **Domain Controller**:

Open:

```
Active Directory Users and Computers
```

Go to:

```
Computers
```

You should see the **client machine listed**.

<img width="1031" height="803" alt="image" src="https://github.com/user-attachments/assets/ea1e76e0-b6f4-40ff-b7f5-3458fd551665" />
