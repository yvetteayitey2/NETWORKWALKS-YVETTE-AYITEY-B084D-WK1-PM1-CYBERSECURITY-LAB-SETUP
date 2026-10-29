# 🔒 Cybersecurity Lab Environment Setup

Building an isolated virtual lab for penetration testing and ethical hacking practice.

![Skill: Cybersecurity](https://img.shields.io/badge/Skill-Cybersecurity-red?style=flat-square) ![Ver: VirtualBox v7.2](https://img.shields.io/badge/Ver-VirtualBox_v7.2-blue?style=flat-square) ![OS: Kali Linux](https://img.shields.io/badge/OS-Kali_Linux_2026.2-orange?style=flat-square) ![Skill: Linux](https://img.shields.io/badge/Skill-Linux-grey?style=flat-square) ![Network: 10.0.0.0/24](https://img.shields.io/badge/Network-10.0.0.0%2F24-teal?style=flat-square) ![Focus: Penetration Testing](https://img.shields.io/badge/Focus-Penetration_Testing-darkred?style=flat-square) ![Skill: Virtualization](https://img.shields.io/badge/Skill-Virtualization-purple?style=flat-square) ![Platform: GitHub](https://img.shields.io/badge/Platform-GitHub-black?style=flat-square)

---
# 📌 Overview

This project shows how I set up a simple cybersecurity laboratory using **VirtualBox** and **Kali Linux** on my **Microsoft Surface Laptop 3** (Intel Core i5, 8 GB RAM).

The main goal of this lab is to create a safe, isolated environment where I can practice network scanning, packet analysis, and vulnerability assessment without affecting my main computer.

I configured the lab on a private virtual network so I can easily add target virtual machines later for authorized security testing.


![Title Overview](1-Screenshot-title-image.png.png)

---
# 🎯 Project Objectives

The primary goals for this setup were to:

* Install and configure VirtualBox as the hypervisor.
* Unpack and import the Kali Linux virtual machine.
* Build a private NAT Network for lab traffic.
* Assign a static IPv4 address to the Kali VM.
* Test local gateway connectivity, internet access, and DNS resolution.
* Save a clean VM snapshot for quick recovery.
*


---
# 🔵 Lab Purpose

This lab gives me an isolated testing environment for learning and practicing core security tasks, such as:

* Network reconnaissance and host discovery
* Port scanning and service enumeration
* Vulnerability assessment
* Packet inspection and analysis
* Web application security testing
* Security tool experimentation

> ⚠️ **Important:** This laboratory is strictly for testing systems I own or have permission to audit. I do not use these tools on unauthorized networks.

---
## 🏗️ **Lab Architecture**

### **Hypervisor: VirtualBox**

| 🔧 Component | ⚙️ Configuration |
| :--- | :--- |
| **Host OS** | **Windows 11** |
| **Host RAM** | **8 GB** |
| **Processor** | **Intel Core i5** |
| **Hypervisor** | **VirtualBox 7.2** |
| **Security OS** | **Kali Linux 2026.2** |
| **Kali RAM** | **2048 MB** |
| **Virtual Network** | **NAT Network (`NatNetwork`)** |
| **Network Address** | **`10.0.0.0/24`** |
| **Kali IP Address** | **`10.0.0.2/24`** |
| **Default Gateway** | **`10.0.0.1`** |
| **DNS Server** | **`8.8.8.8`** |


---
## 🛠️ **Lab Setup Procedure**

### **Step 1. Install 7-Zip**
*   **7-Zip** was installed to extract the Kali Linux virtual-machine package, which may be distributed as a **`.7z` archive**.
*   **Tool:** **7-Zip**

### **Step 2. Install VirtualBox**
*   **VirtualBox** was installed as the hypervisor.

### **Step 3. Create the NAT Network**
*   A dedicated **NAT Network** was created in VirtualBox.
*   **Configuration:** 
    *   **Network Name:** `NatNetwork` 
    *   **IPv4 Prefix:** `10.0.0.0/24` 
    *   **DHCP:** `Enabled` 
    *   **IPv6:** `Disabled`

![Network Settings](2-Screenshot-network-settings-1.png)

### **Step 4. Import Kali Linux**
*   The **Kali Linux virtual machine** was downloaded from the official Kali Linux website and imported into VirtualBox.
*   The VM network adapter was configured as follows:
    *   **Adapter 1:** Attached to **NAT Network** (`NatNetwork`)
    *   **Adapter Type:** **Intel PRO/1000 MT Desktop**
*   The VM was allocated **2048 MB RAM**.

![Kali Linux Desktop](3-Screenshot-kali-linux.png.png)

### **Step 5. Configure the Kali Linux Network**
*   The **Kali Linux network configuration** was checked and configured with a **consistent IPv4 address**.
*   **Example configuration:**
    *   **IP Address:** `10.0.0.2`
    *   **Subnet Mask:** `255.255.255.0`
    *   **Gateway:** `10.0.0.1`
    *   **DNS:** `8.8.8.8`

![Kali Network Settings](4-Screenshot-kali-network-settings.png.png)

### **Step 6. Create a Clean VM Snapshot**
*   After completing the initial configuration, a VirtualBox snapshot was created.
*   **Example snapshot name:** **`fresh-Kali - Network Setup`**
*   The snapshot represents the **clean baseline** of the laboratory. If a future exercise changes or damages the VM configuration, the machine can be restored to this baseline.

---

## 🔬 **Lab Verification**

| 🧪 Test | 💻 Command | 🎯 Expected Result |
| :--- | :--- | :--- |
| **Check IP address** | `ip a` | **Correct Kali IP displayed (`10.0.0.2`)** |
| **Test gateway** | `ping 10.0.0.1` | **Successful replies** |
| **Test Internet connectivity** | `ping 8.8.8.8` | **Successful replies** |
| **Test DNS resolution** | `nslookup networkwalks.com` | **Domain resolves** |
| **Verify Nmap** | `nmap --version` | **Nmap version displayed** |
| **Verify snapshot** | Restore snapshot and run `ip a` | **Baseline configuration restored** |

---

## 🐞 **Problems Encountered & Solutions**

### **Problem 1. Internet Connectivity After Static IP Configuration**
After manually configuring the IPv4 settings, internet connectivity failed on the Kali/NetworkManager configuration.

*   **One workaround used during this lab was:**
    ```bash
    sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
    ```
*   The network connection was then restarted/rebooted and connectivity was tested again.

### 2. Locating Screenshots & Moving Files Out of Kali
* **The Challenge:** Finding where screen captures were saved inside Kali Linux's filesystem and getting them transferred to my main host laptop for documentation.
* **How I Solved It:** Used the Linux terminal to navigate Kali's directory structure, located the saved image files, and transferred them to my host OS using shared clipboard/folder setup.

### 3. Broken Image Links on GitHub (Markdown Case-Sensitivity)
* **The Challenge:** Image previews were breaking on GitHub when previewing my documentation.
* **How I Solved It:** I realized GitHub Markdown is strictly case-sensitive regarding relative file paths. I double-checked every image path and renamed my files to match exact lowercase/uppercase letter cases.

---

# 💡 Key Concepts Learned

1. **NAT vs. NAT Network**
   * A standard NAT connection isolates one VM behind the host. A NAT Network allows multiple VMs on the same virtual network to talk to each other while still routing outbound internet traffic.

2. **Virtual Networking Fundamentals**
   * Learned how virtual network interfaces handle traffic routing between the host OS and virtual machines.

3. **Static IP Configuration**
   * Practiced setting up fixed IPv4 addresses, subnet masks, gateways, and DNS servers inside Linux.

4. **VM Snapshots**
   * Learned to create a clean baseline snapshot before testing tools or changing configuration files.

---

## 🛡️ **Security & Ethical Use**

This laboratory is intended strictly for **education purposes only**.

---

## 🔗 **Tools & Resources**

*   **7-Zip:** [7-zip.org/download.html](https://7-zip.org/download.html)
*   **VirtualBox:** [virtualbox.org/wiki/Downloads](https://virtualbox.org/wiki/Downloads)
*   **Kali Linux:** [kali.org/get-kali](https://kali.org/get-kali)

---

## 👤 **Author**

*   **Yvette Ayitey**
*   **Cybersecurity Internship B084D**
*   **LinkedIn:**[https://www.linkedin.com/in/yvette-ayitey-112a29344?utm_source=share_via&utm_content=profile&utm_medium=member_android]

---

## 📌 **Project Information**

Program Name: **Cybersecurity at Networkwalks** | Week: **01** | Project: **Cybersecurity & Pentesting Lab Setup** | Repository: **GitHub**
