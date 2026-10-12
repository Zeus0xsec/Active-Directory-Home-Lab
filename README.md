# 🛡️ Home Lab – Active Directory Setup

[![PL](https://img.shields.io/badge/Język-Polski-red.svg)](README_PL.md)
[![EN](https://img.shields.io/badge/Language-English-blue.svg)](README.md)

#  Active Directory & Infrastructure Home Lab

##  About the Project
Deployment and configuration of a local virtual environment based on Windows Server 2022 and Windows 11 Enterprise to simulate a corporate infrastructure.

##  Technologies Used
- Windows Server 2022 (Active Directory DS, DNS, GPO, SMB)
- Windows 11 Pro / Enterprise
- Oracle VirtualBox (Internal Network / Isolated Lab)
- PowerShell / CLI


##  Completed Tasks & Evidence (Screenshots)

1. AD DS Configuration and Client Join
Configured the `cyberlab.local` domain controller. The Windows 11 workstation was successfully joined to the domain.
<img width="3429" height="1385" alt="Weryfikacja domeny" src="<img width="3429" height="1385" alt="Weryfikacja domeny" src="https://github.com/user-attachments/assets/f7d08a87-e773-402e-95af-ab9f3ac3fc69" />


2. OU (Organizational Units) Structure
Designed a clear OU structure (`Company` -> `Users` / `Computers`) and moved domain objects.
<img width="3430" height="1385" alt="OU" src="<img width="3430" height="1385" alt="OU" src="https://github.com/user-attachments/assets/dd9cf7de-0782-4daa-a8d3-879c8e019937" />
   

3. Group Policy (GPO) Deployment
Created and enforced a GPO policy blocking access to the Command Prompt for domain users.
<img width="3431" height="1387" alt="Polityka GPO" src="<img width="3431" height="1387" alt="Polityka GPO" src="https://github.com/user-attachments/assets/8e59aeb7-1ced-4f4d-806b-22347f855aac" />
   

4. SMB File Shares and NTFS Permissions
Configured a secure file share `\\DC01\Dane_Firmowe` and mapped it automatically on the workstation.
<img width="3433" height="1386" alt="Zmapowany dysk" src="<img width="3433" height="1386" alt="Zmapowany dysk" src="https://github.com/user-attachments/assets/0efadeb1-5c21-432a-b050-178bef8146ed" />
   


## Phase 2: Wazuh SIEM & Security Monitoring

In the next development phase of my home lab, I focused on deploying the security layer, monitoring (SOC / Blue Team), and alert automation.

### Deployed Components and Configuration
1. **Wazuh SIEM Manager & Agent:** 
   * Deployed the Wazuh manager on an Ubuntu system.
   * Configured the internal network in VirtualBox (`intnet`), along with stable routing and static IP addressing.
   * Successfully connected the Wazuh agent on the domain controller (`DC01`) and verified its active status.
2. **Active Directory Monitoring:**
   * Configured log collection from the Windows Security Event Channel.
   * Tracked key domain events, including the creation of new user accounts and modifications to their attributes (Event IDs `4720`, `4738`, and related).
3. **Notification Pipeline (Postfix + Mailtrap):**
   * Configured a local Postfix mail relay on the Ubuntu machine.
   * Enabled SASL authentication (`smtp_sasl_auth_enable`) and mapped data in the `sasl_passwd` file to meet the security requirements of the external SMTP sandbox (`sandbox.smtp.mailtrap.io`).
   * Automated delivery of Wazuh security alerts directly to the test inbox.

### Evidence and Screenshots
<img width="1710" height="1387" alt="Stan Wazuh" src="https://github.com/user-attachments/assets/8dff5e7d-bbec-4854-9968-88aadc032fa3" />

<img width="1715" height="1386" alt="Logi WS" src="https://github.com/user-attachments/assets/ae07d906-5dbb-41c6-abdc-6561bffadde5" />

<img width="1024" height="830" alt="Logi Wazuh" src="https://github.com/user-attachments/assets/5d536fdb-a297-47d5-9575-9c035c469b97" />

<img width="1024" height="389" alt="MailTrap" src="https://github.com/user-attachments/assets/92214127-1574-4796-8ca4-22f37368a0e2" />


