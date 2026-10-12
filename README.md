# 🛡️ Home Lab – Active Directory Setup

[![PL](https://img.shields.io/badge/Język-Polski-red.svg)](README_PL.md)
[![EN](https://img.shields.io/badge/Language-English-blue.svg)](README.md)

## 🛠️ Module 1: Active Directory Foundation & Infrastructure

The primary goal of this module was to build the core foundation for a Windows-based enterprise environment to simulate real-world SOC and Blue Team scenarios.

#### 1. Domain Controller Setup (DC01)
* Deployed Windows Server to act as the primary Domain Controller.
* Assigned a static IP address (`192.168.10.11`) to ensure network stability for DNS and AD services.
* Promoted the server to a Domain Controller and configured the root domain as `cyberlab.local`.

#### 2. Client Integration
* Deployed a Windows 11 Enterprise virtual machine as the primary endpoint for future attack and defense simulations.
* Successfully joined the Windows 11 client to the `cyberlab.local` domain.

#### 3. Organizational Structure (OU)
* Designed a logical Active Directory structure.
* Created distinct Organizational Units (OUs) such as IT, HR, Sales, and Admins to facilitate granular Group Policy (GPO) targeting and user management.

  <img width="3429" height="1385" alt="Weryfikacja domeny" src="https://github.com/user-attachments/assets/6be06a42-0e19-44c4-a693-1febf14ee581" />
  <img width="3430" height="1385" alt="OU" src="https://github.com/user-attachments/assets/55b9491e-f433-456f-82ce-7b1517932191" />
  <img width="3431" height="1387" alt="Polityka GPO" src="https://github.com/user-attachments/assets/0181da51-5639-4037-a157-99c36bc144b4" />
  <img width="3433" height="1386" alt="Zmapowany dysk" src="https://github.com/user-attachments/assets/07490c7a-2d41-4e74-bf90-67b68373796c" />


