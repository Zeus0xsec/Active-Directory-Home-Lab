# 🏢 Active Directory & Corporate Infrastructure Home Lab

[![PL](https://img.shields.io/badge/Język-Polski-red.svg)](README_PL.md)
[![EN](https://img.shields.io/badge/Language-English-blue.svg)](README.md)

## 📌 Project Overview
This project demonstrates the design and deployment of a fully functional Windows Server Active Directory environment from scratch. It simulates a small corporate network infrastructure using Oracle VirtualBox, focusing on identity management, network services (DNS, DHCP), and security policies.

## ⚙️ Technologies & Tools
* **OS:** Windows Server 2022, Windows 11 (Client)
* **Virtualization:** Oracle VirtualBox
* **Core Services:** Active Directory Domain Services (AD DS), DNS, SMB/NTFS
* **Management & Automation:** Group Policy Objects (GPO), PowerShell

## 🚀 Key Features Configured
* Deployed a Windows Server 2022 Domain Controller (`cyberlab.local`).
* Configured isolated VirtualBox Internal Networking (`intnet`) with static IP addressing.
* Structured Organizational Units (OUs) for realistic company departments (IT, HR, Management).
* Automated the creation of test users using **PowerShell** scripts.
* Implemented **GPO (Group Policy Objects)** to enforce security (e.g., disabling Command Prompt for standard users, mapping network drives).
* Configured NTFS permissions for secure file sharing via SMB.

## 🛠️ Challenges & Troubleshooting (How I solved them)
1. **Network Connectivity & Internet Access on DC:**
   * *Problem:* When assigning a static IP for the internal network, the Domain Controller lost external internet access (needed for updates).
   * *Solution:* I configured dual network adapters (NAT for external, Internal Network for local domain traffic) and adjusted routing metrics in PowerShell so domain traffic stays local while internet traffic routes through NAT.
2. **Client Domain Join Failure (DNS Resolution):**
   * *Problem:* The Windows 11 client machine couldn't find the `cyberlab.local` domain to join it.
   * *Solution:* I identified that the client was using the default VirtualBox DNS. I manually pointed the client's IPv4 DNS settings directly to the static IP of the Domain Controller, which resolved the issue immediately.

## 📸 Screenshots
<img width="3429" height="1385" alt="Weryfikacja domeny" src="https://github.com/user-attachments/assets/23605b19-a545-4585-a6d7-3a3c8ec067e2" />
<img width="3430" height="1385" alt="OU" src="https://github.com/user-attachments/assets/8adad143-59da-49b5-86d2-03ca905aef4b" />
<img width="3431" height="1387" alt="Polityka GPO" src="https://github.com/user-attachments/assets/8b2b4883-1e65-4e0e-8bc6-4206a8aded6d" />
<img width="3433" height="1386" alt="Zmapowany dysk" src="https://github.com/user-attachments/assets/23445728-5926-405d-bb55-df092922526f" />
