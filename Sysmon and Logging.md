In this part, I will install sysmon on the domain controller and my windows 10 client then I will show the setps i took to send all logs from my WAF (Modsecurity), ssh cowrie logs and apache logs for the DVWA(Damn vulnerable web application)
webserver.

# SYSMON INSTALLING ON DC AND CLIENT

# 1️⃣ Download Sysmon

1. Go to the official Microsoft Sysinternals page:
    
    https://learn.microsoft.com/sysinternals/downloads/sysmon
    
2. Click **Download Sysmon**.
3. You will download a file called:

```
Sysmon.zip
```

1. Extract the zip file.

Inside you will see:

```
Sysmon.exe       (64-bit)
Sysmon64.exe
Sysmon64a.exe
Eula.txt
```

Most systems use:

```
Sysmon64.exe
```

---

# 2️⃣ Move Sysmon to a Folder

Create a folder to store Sysmon.

Example:

```
C:\Tools\Sysmon
```

Copy the files into that folder.

---

# 3️⃣ Open Command Prompt as Administrator

1. Press **Start**
2. Search:

```
cmd
```

1. Right-click **Command Prompt**
2. Click **Run as administrator**

Navigate to the folder:

```
cd C:\Tools\Sysmon
```

---

# 4️⃣ Install Sysmon (Basic Install)

Run:

```
Sysmon64.exe -i
```

You will see the **Sysmon license agreement**.

<img width="1907" height="829" alt="image" src="https://github.com/user-attachments/assets/c44a12a9-03d0-4420-b5fb-f1d0fe3eccac" />

Press **Accept**.

Sysmon will install as a **Windows service**.

# 5️⃣ Install Sysmon With a Configuration File (Recommended)

Most security labs use a config file to control logging.

One popular config is from **SwiftOnSecurity**.

Download:

https://github.com/SwiftOnSecurity/sysmon-config

Save the file:

```
sysmonconfig-export.xml
```

Place it in your Sysmon folder.

Install Sysmon with config:

```
Sysmon64.exe -i sysmonconfig-export.xml
```

---

# 6️⃣ Verify Sysmon Installed

Check the service.

Run:

```
sc query sysmon64
```

You should see:

```
STATE: RUNNING
```

---

# 7️⃣ Check Sysmon Logs

Sysmon logs appear in **Windows Event Viewer**.

Open:

```
Event Viewer
```

Navigate to:

```
Applications and Services Logs
   └ Microsoft
       └ Windows
           └ Sysmon
               └ Operational
```

You should start seeing events like:

| Event ID | Description |
| --- | --- |
| 1 | Process Creation |
| 3 | Network Connection |
| 7 | Image Loaded |
| 11 | File Created |
| 22 | DNS Query |

---

# 8️⃣ Test Sysmon

Open **Command Prompt** and run:

```
notepad.exe
```

Then check **Event Viewer → Sysmon → Operational**.

You should see:

```
Event ID 1 – Process Create
```

---

# 9️⃣ Check Sysmon Status

Run:

```
Sysmon64.exe -c
```

This shows the **current configuration**.

---

# 🔟 Update Sysmon Configuration

If you want to change the config:

```
Sysmon64.exe -c sysmonconfig-export.xml
```

<img width="1028" height="802" alt="image" src="https://github.com/user-attachments/assets/53533adc-c3f7-4c1f-915c-211fe7a3798f" />


and after running event viewer in administrator mode , you should see sysmon logs by going to 
Application and services > microsoft > windows > sysmon.
