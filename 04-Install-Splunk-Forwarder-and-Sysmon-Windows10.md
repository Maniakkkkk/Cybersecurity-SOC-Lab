# 🔄 Step 4: Install Splunk Universal Forwarder & Sysmon on Windows 10 Hosts

## 🧠 Objective  
Install and configure the Splunk Universal Forwarder on Windows 10 clients to ship Windows Event Logs to your Splunk Enterprise server, and deploy Sysmon (with Olaf’s configuration) for enriched endpoint telemetry.

---

## 🧰 Requirements  
- Windows 10 Pro VM joined to `ejon.local` domain  
- Splunk Enterprise server reachable at `192.168.10.10:9997` (default UF listening port)  
- Administrative privileges on the Windows 10 hosts  
- Internet access to download installers  

---

## ⚙️ 1. Download Splunk Universal Forwarder

1. On your Windows 10 VM, open a browser and navigate to Splunk’s UF download page:  
   `https://www.splunk.com/en_us/download/universal-forwarder.html`  
2. Download the **Windows 64-bit MSI** installer (e.g. `splunkforwarder-9.x.x-x64-release.msi`).

---

## 💿 2. Install Splunk Universal Forwarder

1. Double‑click the MSI installer.  
2. In the wizard:  
   - Accept the license agreement.  
   - Choose **“Install as a service”**.  
   - Provide an administrator username/password for the Splunk service (you can create a local “splunk” user or use `LocalSystem`).  
3. On the “Configure Splunk Forwarder” screen:  
   - **Manager host**: `192.168.10.10`  
   - **Port**: `9997`  
4. Complete the installation and close the wizard.

---

## 🔧 3. Configure Forwarder Inputs

Edit (or create) the file `%SPLUNK_HOME%\etc\system\local\inputs.conf` to collect Windows event logs:

```ini
[default]
host = WIN10-Client01
index = wineventlog

[WinEventLog://Security]
disabled = 0

[WinEventLog://System]
disabled = 0

[WinEventLog://Application]
disabled = 0
Tip: adjust host= per machine (e.g. WIN10-Client02).

🌐 4. Restart Splunk Forwarder Service
Open an elevated PowerShell prompt and run:

powershell
Copy
Edit
Restart-Service splunkforwarder
Verify connectivity in Splunk Enterprise:

spl
Copy
Edit
index=wineventlog host=WIN10-Client01 | stats count by sourcetype
🖥️ 5. Download & Install Sysmon
Download Sysinternals Sysmon from Microsoft:
https://docs.microsoft.com/sysinternals/downloads/sysmon

Extract Sysmon64.exe to C:\Tools\Sysmon\.

🛠️ 6. Apply Olaf’s Sysmon Configuration
Obtain Olaf’s Sysmon config file (e.g. olaf-sysmon-config.xml).

Place it in C:\Tools\Sysmon\.

Install Sysmon with the configuration:

powershell
Copy
Edit
cd C:\Tools\Sysmon
.\Sysmon64.exe -accepteula -i olaf-sysmon-config.xml
Verify installation:

powershell
Copy
Edit
.\Sysmon64.exe -c
You should see the loaded configuration rules.

