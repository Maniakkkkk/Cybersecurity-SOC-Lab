Here's an enhanced version of your SOC lab project description with a focus on future improvements involving Snort for IDS and IPS:

---

# EJON SOC Lab – Active Directory + Splunk Integration with IDS/IPS Focus

## 🧠 Overview

This project simulates a real-world **Security Operations Center (SOC)** by creating an **Active Directory (AD)** environment and integrating it with **Splunk** on an **Ubuntu Server**. The lab demonstrates log collection, monitoring, and basic alerting from domain-joined Windows machines. Future enhancements will focus on integrating **Intrusion Detection Systems (IDS)** and **Intrusion Prevention Systems (IPS)**, specifically leveraging **Snort**, to detect and respond to network-based threats.

---

## 🛠️ Lab Components

| Component           | Description                                   |
| ------------------- | --------------------------------------------- |
| Windows Server 2022 | Domain Controller (AD DS, DNS, DHCP)          |
| Windows 10 Hosts    | Two endpoint machines joined to the domain    |
| Ubuntu 22.04 Server | Splunk Enterprise installed for log analysis  |
| Splunk Forwarders   | Installed on Windows hosts for log shipping   |
| Snort IDS/IPS       | To be integrated for network threat detection |

---

## ⚙️ Implementation Summary

### ✅ Active Directory Setup

* Installed and configured AD DS, DNS, and DHCP
* Created domain: `ejon.local`
* Added users and organizational units (OUs)

### ✅ Domain Join

* Joined two Windows 10 Pro hosts to the domain
* Verified Group Policy Object (GPO) application and domain logins

### ✅ Splunk Setup on Ubuntu

* Installed Splunk Enterprise on Ubuntu Server
* Configured listening port and admin credentials
* Enabled web interface (port 8000)

### ✅ Log Forwarding

* Installed **Splunk Universal Forwarder** on both Windows hosts
* Configured inputs to forward Security, System, and Application logs to Splunk
* Verified log ingestion in Splunk via SPL searches

### ✅ Future IDS/IPS Integration with Snort

* **IDS Integration**: Plan to deploy Snort on Ubuntu to monitor network traffic for suspicious activity and potential threats.
* **IPS Setup**: Once Snort IDS is operational, will configure IPS functionality to actively block detected malicious activities in real time.
* **Splunk-Snort Correlation**: Forward Snort-generated alerts to Splunk to correlate with system and security logs for advanced detection and response.

---

## 🧠 Key Takeaways

* Built a functional SOC lab with Active Directory and Splunk integration
* Gained hands-on experience in integrating endpoint telemetry with Splunk
* Developed an understanding of Windows event log analysis
* Laid the groundwork for future IDS/IPS integration with Snort to enhance network security

---

## 💡 Future Enhancements

1. **IDS/IPS Integration with Snort**: Focus on adding Snort as the primary IDS/IPS solution to detect and block network-based threats in real time.

2. **Host-based IPS with OSSEC or Wazuh**: Implement OSSEC or Wazuh agents on Windows and Linux hosts to extend intrusion prevention and file integrity monitoring across endpoints.

3. **MITRE ATT\&CK Automation**: Automate the mapping of alerts to MITRE tactics using **Splunk Enterprise Security** to improve incident analysis and response times.

4. **SOAR Integration**: Implement automated incident response workflows using **Splunk SOAR** (formerly Phantom) for efficient and effective incident handling.

5. **Threat Intelligence Feeds**: Integrate threat intelligence feeds (such as **MISP** and **OTX**) into Splunk for enriched detection and response.

6. **Network Traffic Dashboards**: Create visual dashboards to monitor network traffic and correlate Snort IDS alerts with **Sysmon** events to identify advanced threats.

7. **Performance Optimization**: Optimize the performance of the lab by tuning index retention policies, enhancing forwarding performance, and scaling the setup for larger networks.

---

**Ejon Rexhepi, Republic of Kosovo**
Security Operations | Cyber Threat Intelligence

**LinkedIn**: [www.linkedin.com/in/ejon-rexhepi-er04412](https://www.linkedin.com/in/ejon-rexhepi-er04412)

