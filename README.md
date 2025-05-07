# Cybersecurity-SOC-Lab
 SOC lab project with AD and Splunk on Ubuntu

# EJON SOC Lab – Active Directory + Splunk Integration

## 🧠 Overview

This project simulates a real-world **Security Operations Center (SOC)** by creating an Active Directory (AD) environment and integrating it with **Splunk** on a **Ubuntu Server**. It demonstrates log collection, monitoring, and basic alerting from domain-joined Windows machines.

---

## 🛠️ Lab Components

| Component           | Description                                  |
|---------------------|----------------------------------------------|
| Windows Server 2022 | Domain Controller (AD DS, DNS, DHCP)         |
| Windows 10 Hosts    | Two endpoint machines joined to the domain   |
| Ubuntu 22.04 Server | Splunk Enterprise installed for log analysis |
| Splunk Forwarders   | Installed on Windows hosts for log shipping  |

---

## ⚙️ Implementation Summary

### ✅ Active Directory Setup
- Installed and configured AD DS, DNS, and DHCP
- Created domain: `ejon.local`
- Added users and organizational units

### ✅ Domain Join
- Joined two Windows 10 Pro hosts to the domain
- Verified GPO application and domain logins

### ✅ Splunk Setup on Ubuntu
- Installed Splunk Enterprise on Ubuntu Server
- Configured listening port and admin credentials
- Enabled web interface (port 8000)

### ✅ Log Forwarding
- Installed **Splunk Universal Forwarder** on both Windows hosts
- Configured inputs to forward Security, System, and Application logs
- Verified log ingestion in Splunk via SPL searches

---

## 🧠 Key Takeaways

- Built a fully functional SOC lab from scratch
- Practiced integrating endpoint telemetry with Splunk
- Gained hands-on experience analyzing Windows event logs
💡 Future Improvements

Implement Intrusion Detection Systems (IDS): Integrate Suricata or Snort to detect network-based threats and forward alerts to Splunk.

Add Host-based IPS: Deploy OSSEC or Wazuh agents on Windows and Linux hosts for real-time host intrusion prevention and file integrity monitoring.

MITRE ATT&CK Automation: Automate mapping of alerts to MITRE tactics using Splunk Enterprise Security.

SOAR Integration: Implement automated incident response workflows with Splunk SOAR or Phantom.

Threat Intelligence Feeds: Add additional feeds (MISP, OTX) and automate blocking of malicious IPs via firewall scripts.

Network Visualization: Use network traffic dashboards to visualize IDS alerts and correlate with Sysmon events.

Performance Tuning: Optimize index retention, indexing rate, and forwarder performance for large-scale deployment.

---
Ejon Rexhepi, Republic of Kosovo
Security Operations | Cyber Threat Intelligence



