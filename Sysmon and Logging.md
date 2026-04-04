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

<img width="1028" height="802" alt="image" src="https://github.com/user-attachments/assets/53533adc-c3f7-4c1f-915c-211fe7a3798f" />


and after running event viewer in administrator mode , you should see sysmon logs by going to 
Application and services > microsoft > windows > sysmon.


# SENDINGS LOGS TO SPLUNK




## --Sending cowrie logs to Splunk.


### 1️⃣ Confirm Where Cowrie Logs Are Stored

Cowrie stores logs in:

~/cowrie/var/log/cowrie/
​
You should see files like:

cowrie.json

cowrie.log
​
<img width="1178" height="762" alt="image" src="https://github.com/user-attachments/assets/ee8a9dff-b66a-4057-b18a-be53af6c48f1" />


The important one for Splunk is:

cowrie.json
​
Check it:

cat ~/cowrie/var/log/cowrie/cowrie.json
​
You should see JSON attack events.

### 2️⃣ Install the Splunk Universal Forwarder

Download the forwarder from Splunk:

https://www.splunk.com/en_us/download/universal-forwarder.html

Choose:

Linux (.deb) 64-bit
​
<img width="1166" height="757" alt="image" src="https://github.com/user-attachments/assets/301d788b-0b85-4ca2-990f-068639314211" />


Install it:

sudo dpkg-i splunkforwarder*.deb
​
<img width="1184" height="763" alt="image" src="https://github.com/user-attachments/assets/ce75e912-9e37-4e70-94aa-fa87450e5eff" />


Fix dependencies if needed:

sudo apt--fix-broken install
​
### 3️⃣ Start the Splunk Forwarder
Run:

sudo /opt/splunkforwarder/bin/splunkstart
​
Accept the license:

```
y
​
```

Create admin credentials.

### 4️⃣ Connect the Forwarder to Your Splunk Server

Tell the forwarder where your Splunk server is.

Example (replace IP with your Splunk server):

sudo /opt/splunkforwarder/bin/splunk add forward-server SPLUNK_IP:9997
​
Example:

sudo /opt/splunkforwarder/bin/splunk add forward-server192.168.1.50:9997
​
9997 is the default Splunk receiving port.

### 5️⃣ Tell Splunk to Monitor Cowrie Logs
Run:

sudo /opt/splunkforwarder/bin/splunk add monitor 

~/cowrie/var/log/cowrie/cowrie.json
​
This tells Splunk:

Monitor Cowrie attack logs

Send them to Splunk server
​
### 6️⃣ Restart the Forwarder

sudo /opt/splunkforwarder/bin/splunkrestart
​
### 7️⃣ Enable Forwarder at Boot

sudo /opt/splunkforwarder/bin/splunk enable boot-start
​
### 8️⃣ Verify Logs Are Reaching Splunk

Open the Splunk web interface:

http://SPLUNK_SERVER_IP:8000
​
Go to:

Search & Reporting
​
Run this search:

source="*cowrie.json"
​
<img width="1176" height="769" alt="image" src="https://github.com/user-attachments/assets/adb7ad61-4ec6-4563-92ef-5ae538c034eb" />


YOU SHOULD BE SEING COWIRE LOGS NOW

<img width="1299" height="831" alt="image" src="https://github.com/user-attachments/assets/9ef65f15-f7d2-4a65-af6a-22cda37fab2a" />


## —-SENDING DVWA AND MODSECURITY LOGS TO SPLUNK

### 1️⃣ Find the DVWA / Apache Logs

DVWA usually runs on Apache, so the logs are the Apache access and error logs.

Typical locations:

/var/log/apache2/access.log

/var/log/apache2/error.log
​
Check them:

sudo tail-f /var/log/apache2/access.log
​
When someone visits DVWA you should see requests like:

192.168.1.10 - - "GET /dvwa/login.php HTTP/1.1"
​
### 2️⃣ Find the ModSecurity Logs

ModSecurity logs usually appear in:

/var/log/apache2/modsec_audit.log
​
or

/var/log/modsec_audit.log
​
Check:

sudo tail-f /var/log/apache2/modsec_audit.log
​
Example event:

ModSecurity: Warning. Pattern match detected SQL injection attack
​
### 3️⃣ Add DVWA Logs to the Splunk Forwarder

Tell the forwarder to monitor the Apache access log:

sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/apache2/access.log
​
the Apache error log:

sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/apache2/error.log
​
### 4️⃣ Add ModSecurity Logs

Add the ModSecurity audit log:

sudo /opt/splunkforwarder/bin/splunk add monitor 

/var/log/apache2/modsec_audit.log
​
If your file is here instead:

sudo /opt/splunkforwarder/bin/splunk add monitor /var/log/modsec_audit.log
​
### 5️⃣ Restart the Forwarder

<img width="1167" height="771" alt="image" src="https://github.com/user-attachments/assets/d14a7903-a14d-400c-b5f3-4650c9f5f4bc" />


sudo /opt/splunkforwarder/bin/splunkrestart
​
### 6️⃣ Verify Logs Are Being Sent

Go to your Splunk Web Interface:

http://YOUR_SPLUNK_IP:8000
​
  Go to Search & Reporting.

### 7️⃣ Search for Apache / DVWA Logs

Run:

source="/var/log/apache2/access.log"
​
You should see HTTP requests.

Example fields:

client IP

URL

HTTP method

status code

user agent
​
Example query:
 
 source="/var/log/apache2/access.log" | stats count by clientip
​
  Shows who is attacking your DVWA.

### 8️⃣ Search for ModSecurity Alerts

Run:

source="*modsec_audit.log"
​
Example query:

source="*modsec_audit.log" | stats count by rule_id
​

  This shows which WAF rules are triggered.

now we should see all the logs in splunk.

## Sending Sysmon and Win-event logs to Splunk(In work)
