# 🔄 Step 3: Install Splunk Forwarder, Sysmon & Configure inputs.conf

## 🧠 Objective

Download and install Splunk Universal Forwarder and Sysmon on Windows 10 hosts, apply Olaf’s Sysmon configuration for enhanced logging, then create an `inputs.conf` file under the Splunk Forwarder local directory to forward Windows and Sysmon event logs to your SOC.

---

## ⚙️ 1. Download & Install Splunk Universal Forwarder

1. On the Windows 10 VM, browse to Splunk UF download page:
   `https://www.splunk.com/en_us/download/universal-forwarder.html`
2. Download the **Windows 64-bit MSI** installer.
3. Run the MSI as Administrator.

   * Accept the license.
   * Choose **Install as a service**.
   * On “Configure Splunk Forwarder,” set **Manager host** to `192.168.10.10` and **Port** to `9997`.
4. Complete installation.

---

## 💿 2. Download & Install Sysmon

1. Download Sysmon from Microsoft Sysinternals:
   `https://docs.microsoft.com/sysinternals/downloads/sysmon`
2. Extract `Sysmon64.exe` to `C:\Tools\Sysmon\`.
3. Place Olaf’s Sysmon configuration file (`olaf-sysmon-config.xml`) into the same folder.
4. In an elevated PowerShell prompt, install Sysmon with Olaf’s config:

   ```powershell
   cd C:\Tools\Sysmon
   .\Sysmon64.exe -accepteula -i olaf-sysmon-config.xml
   ```

---

## 📝 3. Create `inputs.conf` for Splunk Forwarder

1. Open File Explorer as Administrator and navigate to:

   ```text
   C:\Program Files\SplunkUniversalForwarder\etc\system\local
   ```
2. Create a new file named `inputs.conf` and paste the following content:

   ```ini
   [WinEventLog://Application]
   index = endpoint
   disabled = false

   [WinEventLog://Security]
   index = endpoint
   disabled = false

   [WinEventLog://System]
   index = endpoint
   disabled = false

   [WinEventLog://Microsoft-Windows-Sysmon/Operational]
   index = endpoint
   disabled = false
   renderXml = true
   source = XmlWinEventLog:Microsoft-Windows-Sysmon/Operational
   ```
3. Save and close the file.

---

## 🔄 4. Restart Splunk Forwarder Service

In an elevated PowerShell window:

```powershell
Restart-Service splunkforwarder
```

---

## ✅ Outcome

* Splunk UF and Sysmon are installed with Olaf’s configuration.
* The Forwarder is now shipping Application, Security, System, and Sysmon operational logs into the `endpoint` index on your Splunk server.

---

## 🔜 Next Steps

* In Splunk Enterprise, verify data ingestion:

  ```spl
  index=endpoint sourcetype="XmlWinEventLog:Microsoft-Windows-Sysmon/Operational" | head 10
  ```
* Build dashboards and alerts based on the `endpoint` index events.
