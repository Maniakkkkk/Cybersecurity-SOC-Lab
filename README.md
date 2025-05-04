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
- Developed dashboards and alerts for critical security events

---

## 📁 Project Structure




