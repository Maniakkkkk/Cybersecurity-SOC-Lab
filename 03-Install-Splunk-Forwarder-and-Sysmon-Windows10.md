**# 🖥️ Step 1: Install Splunk Forwarder, Sysmon & Configure inputs.conf [local]**

🧠 Objective

Download and install Splunk Universal Forwarder and Sysmon on Windows 10 hosts, apply Olaf’s Sysmon configuration for enhanced logging, then create an inputs.conf file under the Splunk Forwarder local directory to forward Windows and Sysmon event logs to your SOC.


⚙️ 1. Download & Install Splunk Universal Forwarder

On the Windows 10 VM, browse to Splunk UF download page:https://www.splunk.com/en_us/download/universal-forwarder.html

Download the Windows 64-bit MSI installer.

Run the MSI as Administrator.

Accept the license.

Choose Install as a service.

On “Configure Splunk Forwarder,” set Manager host to 192.168.10.10 and Port to 9997.

Complete installation.

💿 2. Download & Install Sysmon

Download Sysmon from Microsoft Sysinternals:https://docs.microsoft.com/sysinternals/downloads/sysmon

Extract Sysmon64.exe to C:\Tools\Sysmon\.

Place Olaf’s Sysmon configuration file (olaf-sysmon-config.xml) into the same folder.

In an elevated PowerShell prompt, install Sysmon with Olaf’s config:

cd C:\Tools\Sysmon
.\Sysmon64.exe -accepteula -i olaf-sysmon-config.xml

📝 3. Create inputs.conf for Splunk Forwarder

Open File Explorer as Administrator and navigate to:

C:\Program Files\SplunkUniversalForwarder\etc\system\local

Create a new file named inputs.conf and paste the following content:

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

Save and close the file.

🔄 4. Restart Splunk Forwarder Service

In an elevated PowerShell window:

Restart-Service splunkforwarder
