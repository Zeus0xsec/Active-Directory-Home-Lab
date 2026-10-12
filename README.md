# 🛡️ Active Directory & Infrastructure Home Lab

[![PL](https://img.shields.io/badge/Język-Polski-red.svg)](README_PL.md)
[![EN](https://img.shields.io/badge/Language-English-blue.svg)](README.md)

##  About the Project
Deployment and configuration of a local virtual environment based on Windows Server 2022 and Windows 11 Enterprise to simulate a corporate infrastructure.

##  Technologies Used
- Windows Server 2022 (Active Directory DS, DNS, GPO, SMB, DHCP)
- Windows 11 Pro / Enterprise
- Oracle VirtualBox (Internal Network / Isolated Lab)
- PowerShell / CLI
- Wazuh SIEM / Sysmon / Postfix / Discord Webhooks


##  Completed Tasks & Evidence (Screenshots)

1. AD DS Configuration and Client Join
Configured the `cyberlab.local` domain controller. A Windows 11 workstation was successfully joined to the domain.
<img width="3429" height="1385" alt="Domain verification" src="https://github.com/user-attachments/assets/f7d08a87-e773-402e-95af-ab9f3ac3fc69" />


2. OU Structure (Organizational Units)
Designed a clear OU structure (`Company` -> `Users` / `Computers`) and moved domain objects.
<img width="3430" height="1385" alt="OU Structure" src="https://github.com/user-attachments/assets/dd9cf7de-0782-4daa-a8d3-879c8e019937" />
   

3. GPO Implementation (Group Policy Objects)
Created and enforced a GPO blocking Command Prompt access for domain users.
<img width="3431" height="1387" alt="GPO Policy" src="https://github.com/user-attachments/assets/8e59aeb7-1ced-4f4d-806b-22347f855aac" />
   

4. SMB File Shares and NTFS Permissions
Configured a secure `\\DC01\Company_Data` file share and mapped it automatically on the workstation.
<img width="3433" height="1386" alt="Mapped drive" src="https://github.com/user-attachments/assets/0efadeb1-5c21-432a-b050-178bef8146ed" />
   

## Phase 2: Wazuh SIEM & Security Monitoring

In the next stage of my home lab development, I focused on implementing the security layer, monitoring (SOC / Blue Team), and notification automation.

### Implemented Components and Configuration
1. **Wazuh SIEM Manager & Agent:** 
   * Deployed the Wazuh manager on an Ubuntu system.
   * Configured the internal network in VirtualBox (`intnet`) alongside stable routing and static IP addressing.
   * Successfully connected the Wazuh agent on the domain controller (`DC01`) and verified its active status.
2. **Active Directory Monitoring:**
   * Configured log collection from the Windows Security Event Channel.
   * Tracked key domain events, including the creation of new user accounts and modifications of their attributes (Event IDs `4720`, `4738`, and related).
3. **Notification Pipeline (Postfix + Mailtrap):**
   * Configured a local Postfix mail relay on the Ubuntu machine.
   * Enabled SASL authentication (`smtp_sasl_auth_enable`) and mapped credentials in the `sasl_passwd` file to meet the security requirements of the external SMTP sandbox (`sandbox.smtp.mailtrap.io`).
   * Automated the delivery of Wazuh security alerts directly to the test inbox.

### Evidence and Screenshots
<img width="1710" height="1387" alt="Wazuh Status" src="https://github.com/user-attachments/assets/8dff5e7d-bbec-4854-9968-88aadc032fa3" />

<img width="1715" height="1386" alt="Windows Logs" src="https://github.com/user-attachments/assets/ae07d906-5dbb-41c6-abdc-6561bffadde5" />

<img width="1024" height="830" alt="Wazuh Logs" src="https://github.com/user-attachments/assets/5d536fdb-a297-47d5-9575-9c035c469b97" />

<img width="1024" height="389" alt="MailTrap" src="https://github.com/user-attachments/assets/92214127-1574-4796-8ca4-22f37368a0e2" />


## Phase 3: Network Architecture, GPO Hardening, and Advanced Monitoring

Today, I focused on deploying the full network architecture, strict environment hardening, and integrating an advanced SOC alert pipeline.

### Implemented Components and Configuration
1. **DHCP Service (Windows Server):** 
   * Configured a DHCP server with an IP address scope (192.168.10.20–100).
   * Set a secure buffer for the domain controller's static IP (.11), ensuring dynamic yet controlled configuration for machines in the internal network.
2. **New Client and Domain Infrastructure:**
   * Connected a new workstation (Windows 11 Enterprise), which successfully obtained DHCP addressing and DNS entries.
   * Successfully joined the machine to the `cyberlab.local` domain and tested direct logins using the created employee accounts.
3. **Advanced OU Structure and Identity Management:**
   * Separated Active Directory users into dedicated organizational units (IT, HR, Sales, Admins).
   * Applied and tested password policies, account lockouts, and reset procedures.
4. **GPO Hardening (Group Policy Objects):**
   * Deployed a GPO blocking the Control Panel for regular employees.
   * Successfully restricted permissions on workstations and successfully tested the enforcement of applied restrictions.
5. **Advanced Monitoring (Sysmon + Wazuh + Discord):**
   * Expanded the alert pipeline: integrated events generated by Sysmon.
   * Configured alerts so that high-severity rules (level > 8) are instantly delivered not only to the Wazuh dashboard but also as real-time notifications to a dedicated Discord channel.

### Evidence and Screenshots
<img width="1021" height="851" alt="DHCP DOWOD" src="https://github.com/user-attachments/assets/858b2a32-0694-439d-be2f-c6bbf8f8e2ac" />
<img width="1714" height="1390" alt="DHCP" src="https://github.com/user-attachments/assets/19f8067f-c078-4c87-869e-ad9ada48cc28" />
<img width="1017" height="846" alt="PRACOWNIK" src="https://github.com/user-attachments/assets/a6dc35eb-ec7b-4c35-9d12-8f28f19f7392" />
<img width="1714" height="1389" alt="AD" src="https://github.com/user-attachments/assets/0859c2c6-3579-44e3-8780-235ccb77abff" />
<img width="1713" height="1325" alt="SYSMON" src="https://github.com/user-attachments/assets/c74bfe75-9f69-417d-9f0c-9e6d39b3c2d1" />
<img width="1023" height="809" alt="LOGI SYSMON" src="https://github.com/user-attachments/assets/e64a5a79-0f9a-4744-b15f-522a3088495b" />
<img width="2190" height="1273" alt="LOGI DC" src="https://github.com/user-attachments/assets/6945ebaf-7c51-47da-808c-d6aed050741b" />

