# 🖥️ Step 1: Install and Promote Active Directory Server 2022

## 🧠 Objective

This step guides you through installing **Windows Server 2022**, promoting it to a **Domain Controller** for the **ejon.local** domain, setting up DNS, and assigning it a static IP of `192.168.10.11`.

---

## 🧰 Requirements

- A machine or VM running **Windows Server 2022**
- Access to the **Windows Server 2022 ISO**
- A minimum of **2 GB RAM** and **30 GB storage** for the server VM
- Basic networking knowledge (static IP configuration)

---

## 🌐 1. Download Windows Server 2022 ISO

1. Visit the [Microsoft Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server) to download the Windows Server 2022 ISO.
2. Select the **Windows Server 2022** version that fits your needs (Standard or Datacenter).
3. Download the **ISO** file.

---

## 🖥️ 2. Set Up Virtual Machine

1. Open **VirtualBox** (or another VM software).
2. Click **New** and create a new VM with the following settings:
   - **Name**: `Windows-Server-2022`
   - **Type**: `Microsoft Windows`
   - **Version**: `Windows 2019 (64-bit)`
   - **Memory**: Allocate **2-4 GB** of RAM
   - **Disk Size**: Create a **dynamically allocated** disk with at least **50 GB** of storage
3. Mount the **Windows Server 2022 ISO** under **Settings > Storage**.

---

## 💿 3. Install Windows Server 2022

1. Start the VM and follow the installation prompts:
   - Choose your **language** and **keyboard**.
   - Click **Install Now**.
   - Select **Windows Server 2022 Standard** for installation.
   - Choose **Custom Installation** and select the virtual disk.
   
2. After the installation is complete, the system will reboot. Set the **Administrator** password when prompted.

---

## 🔧 4. Configure Static IP Address

1. After the installation, log in with the **Administrator** account.
2. Go to **Control Panel > Network and Sharing Center > Change adapter settings**.
3. Right-click the **Ethernet** adapter and select **Properties**.
4. Select **Internet Protocol Version 4 (TCP/IPv4)** and click **Properties**.
5. Set the **static IP address**:
   - **IP Address**: `192.168.10.11`
   - **Subnet Mask**: `255.255.255.0`
   - **Default Gateway**: `192.168.10.1` (your router or gateway IP)
   - **DNS Server**: `192.168.10.11` (this server itself for internal DNS)

---

## 🏗️ 5. Promote Server to Domain Controller

1. Open **Server Manager** → Click **Add roles and features**.
2. In the wizard, select **Role-based or feature-based installation**, then choose your server.
3. In the **Roles** section, select **Active Directory Domain Services** and install it.
4. After installation, click the notification to **Promote this server to a domain controller**.
5. In the promotion wizard:
   - Select **Add a new forest** and set the **Root domain name** as `ejon.local`.
   - Set the **Domain Controller functional level** to **Windows Server 2022**.
   - Set the **Directory Services Restore Mode (DSRM)** password.
6. Click **Install** and allow the server to reboot once the promotion is complete.

---

## 🔄 6. Restart and Finalize

1. After the reboot, your server is now the Domain Controller for **ejon.local**.
2. Log in using **Administrator** and the password you set earlier.
3. You can now verify that the DNS is working by running the following command:

```bash
nslookup ejon.local
