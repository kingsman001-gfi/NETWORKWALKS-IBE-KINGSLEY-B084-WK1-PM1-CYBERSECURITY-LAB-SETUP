# CYBERSECURITY-LAB-SETUP
Cybersecurity Lab Setup using VirtualBox to setup Kali LInux for Pentesting and other Cybersecurity Operations


## 📌 Project Overview
This project focuses on setting up a virtual cybersecurity and penetration-testing laboratory using Oracle VirtualBox and Kali Linux. 

The purpose of the lab is to create a controlled environment where cybersecurity tools, network scanning, reconnaissance, vulnerability assessment, and other security-testing activities can be performed safely and repeatedly. The lab is configured on a private virtual network so that additional machines can be added later and used as targets for authorized security testing.

## 🎯 Objectives
The main objectives of this project are to:
- Install and configure VirtualBox.
- Import Kali Linux as a virtual machine.
- Create a private NAT Network for the cybersecurity lab.
- Configure network connectivity for Kali Linux.
- Assign a consistent IP address to the Kali VM.
- Verify network connectivity and DNS resolution.
- Take a clean VM snapshot for recovery.
- Document the complete setup process.
- Prepare the environment for future cybersecurity projects.

## 🛡️ Purpose of the Lab
The lab provides an isolated and controlled environment for cybersecurity learning and authorized security testing, supporting activities such as:
- Network reconnaissance
- Port scanning
- Vulnerability assessment
- Packet analysis
- Web security testing
- Exploitation practice
- Security-tool experimentation

> **⚠️ Important:** This laboratory must only be used for systems that you own or have explicit permission to test. Do not use the lab or its tools to attack unauthorized systems.


## ⚙️ Lab Configuration

| Component | Configuration |
| :--- | :--- |
| **Host OS** | Windows |
| **Hypervisor** | Oracle VirtualBox |
| **Security OS** | Kali Linux |
| **Virtual Network** | NAT Network |
| **Network Address** | 10.0.0.0/24 |
| **Kali IP Address** | 10.0.0.2/24 |
| **Default Gateway** | 10.0.0.1 |
| **DNS Server** | 8.8.8.8 |
| **Future VM Range** | 10.0.0.3–10.0.0.99 |

## 🪜 Lab Setup Procedure

### Step 1. Install VirtualBox
Oracle VirtualBox was installed as the hypervisor to manage virtual machines.

### Step 2. Create the NAT Network
A dedicated NAT Network was created in VirtualBox with the following parameters:
- **Network Name:** NatNetwork
- **IPv4 Prefix:** 10.0.0.0/24
- **DHCP:** Enabled
- **IPv6:** Disabled

*A NAT Network was selected because multiple virtual machines connected to it can communicate with one another while also having outbound network connectivity.*

### Step 3. Import Kali Linux
The Kali Linux virtual machine was imported into VirtualBox and configured:
- **Adapter 1:** Attached to `NAT Network` (NatNetwork)
- **Adapter Type:** Intel PRO/1000 MT Desktop
- A shared folder was also configured for file transfers between the host and guest OS.

### Step 4. Configure the Kali Linux Network
The Kali Linux network configuration was updated with a consistent static IPv4 address (`10.0.0.2/24`) to make future lab referencing reliable.

### Step 5. Create a Clean VM Snapshot
After initial configuration, a VirtualBox snapshot named **`Clean Kali - Network Setup`** was created to serve as a baseline recovery point.

---

## 🔎 Lab Verification

| Test | Command | Expected Result |
| :--- | :--- | :--- |
| **Check IP address** | `ip a` | Correct Kali IP displayed (`10.0.0.2`) |
| **Test gateway** | `ping 10.0.0.1` | Successful replies |
| **Test Internet connectivity** | `ping 8.8.8.8` | Successful replies |
| **Test DNS resolution** | `nslookup networkwalks.com` | Domain resolves successfully |
| **Verify Nmap** | `nmap --version` | Nmap version displayed |

---

## 🐞 Problems Encountered & Solutions

### Problem 1. Internet Connectivity After Static IP Configuration
- **Issue:** Manual IPv4 configuration occasionally caused connectivity drops due to NetworkManager handling.
- **Solution:** Applied the NetworkManager workaround via terminal:
  ```bash
  sudo nmcli connection modify "Wired connection 1" ipv4.dad-timeout 0
Restarted the connection and verified network restoration.

Problem 2. VirtualBox Virtualization Error
Issue: The VM initially failed to boot due to disabled hardware virtualization in BIOS.

Solution: Entered system UEFI/BIOS settings, enabled Intel VT-x / hardware virtualization, saved, and rebooted the host machine.

💡 What I Learned
NAT vs. NAT Network: Learned how standard NAT differs from a NAT Network, enabling multi-VM communication for labs.

Virtual Machine Networking: Understood hypervisor virtual adapters and packet routing.

Static IP Configuration: Gained practical experience managing IPv4 addressing and DNS inside Linux.

VM Snapshots: Realized the critical value of creating clean baseline snapshots before performing testing or modifications.

Technical Documentation: Appreciated the importance of clean logging and structured project documentation.

🔗 Tools & Resources
VirtualBox Downloads

Kali Linux Get-Kali

👤 Author
Name: Ibe Kingsley 

Program: Cybersecurity at Networkwalks (Batch B084)

Project: Week 1 - Cybersecurity & Pentesting Lab Setup
