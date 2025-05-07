


📘 02-Splunk-Install-Ubuntu.md
markdown
Copy
Edit
# 🐧 Step 2: Installing Splunk Enterprise on Ubuntu Server

## 🧠 Objective
Install Splunk Enterprise on a dedicated Ubuntu Server (22.04+) inside VirtualBox, configure static IP, mount shared folders, and enable Splunk for boot-time startup.

---

## ⚙️ 1. System Update & Guest Tools Installation

```bash
sudo apt-get update && sudo apt-get upgrade -y
sudo apt-get install virtualbox-guest-additions-iso virtualbox-guest-utils -y
📂 2. Shared Folder Setup
bash
Copy
Edit
mkdir ~/share
sudo adduser ejon vboxsf  # Replace 'ejon' with your actual username
sudo mount -t vboxsf -o uid=1000,gid=1000 EJON-SOC-Lab ~/share
📝 EJON-SOC-Lab is the name of your VirtualBox shared folder.

🌐 3. Configure Static IP with Netplan
Edit the file /etc/netplan/00-installer-config.yaml with the following configuration:

yaml
Copy
Edit
network:
  version: 2
  ethernets:
    enp0s3:
      dhcp4: no
      addresses: [192.168.10.10/24]
      gateway4: 192.168.10.1
      nameservers:
        addresses: [8.8.8.8, 1.1.1.1]
Then apply the changes:

bash
Copy
Edit
sudo netplan apply
🔁 4. Reboot to Apply Group/Network Changes
bash
Copy
Edit
sudo reboot
📦 5. Download and Install Splunk Enterprise
bash
Copy
Edit
cd ~
wget -O splunk.deb 'https://download.splunk.com/products/splunk/releases/9.2.1/linux/splunk-9.2.1-ae6821f0b3f3-linux-2.6-amd64.deb'
sudo dpkg -i splunk.deb
🚀 6. Start and Enable Splunk
bash
Copy
Edit
cd /opt/splunk
sudo -u splunk bash -c "./splunk start"  # Accept license and create admin user
sudo ./splunk enable boot-start -user splunk
📌 Notes
Splunk Web Interface will be accessible at:
http://192.168.10.10:8000

Default Splunk port: 8000 (web), 8089 (management)

Make sure firewall/VM NAT settings allow external access if needed

✅ Outcome
You now have Splunk Enterprise running on Ubuntu, reachable via browser, and ready to receive logs from Windows domain-joined machines in your SOC lab.
