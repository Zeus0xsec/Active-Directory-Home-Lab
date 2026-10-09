# 🏢 Środowisko Active Directory i Infrastruktura (Home Lab)

[![PL](https://img.shields.io/badge/Język-Polski-red.svg)](README_PL.md)
[![EN](https://img.shields.io/badge/Language-English-blue.svg)](README.md)

## 📌 Cel Projektu
Projekt prezentuje budowę w pełni funkcjonalnego środowiska domenowego Active Directory od zera. Symuluje infrastrukturę sieciową małej firmy przy użyciu Oracle VirtualBox, skupiając się na zarządzaniu tożsamością, usługach sieciowych oraz wdrażaniu polityk bezpieczeństwa.

## ⚙️ Technologie i Narzędzia
* **Systemy:** Windows Server 2022, Windows 11 (Klient)
* **Wirtualizacja:** Oracle VirtualBox
* **Główne Usługi:** Active Directory Domain Services (AD DS), DNS, SMB/NTFS
* **Zarządzanie:** Zasady Grupy (GPO), PowerShell

## 🚀 Zrealizowane Zadania
* Wdrożenie Kontrolera Domeny (`cyberlab.local`) na Windows Server 2022.
* Konfiguracja izolowanej sieci wewnętrznej w VirtualBox z wykorzystaniem statycznego adresowania IP.
* Zbudowanie struktury jednostek organizacyjnych (OU) dla różnych działów firmy.
* Wykorzystanie skryptów **PowerShell** do zautomatyzowanego tworzenia użytkowników.
* Wdrożenie **Zasad Grupy (GPO)** w celu zwiększenia bezpieczeństwa (np. blokada Wiersza Poleceń dla zwykłych użytkowników).
* Konfiguracja bezpiecznych udziałów sieciowych z użyciem uprawnień NTFS i SMB.

## 🛠️ Problemy i jak je rozwiązałem (Troubleshooting)
1. **Brak dostępu do internetu na Kontrolerze Domeny:**
   * *Problem:* Po ustawieniu statycznego IP dla sieci wewnętrznej, serwer stracił dostęp do internetu.
   * *Rozwiązanie:* Skonfigurowałem dwie karty sieciowe (NAT do internetu i Sieć Wewnętrzną do domeny) oraz dostosowałem priorytety routingu w PowerShell, aby ruch domenowy nie wychodził na zewnątrz.
2. **Błąd dołączania stacji klienckiej do domeny (Problem z DNS):**
   * *Problem:* Maszyna z Windows 11 nie mogła odnaleźć domeny `cyberlab.local`.
   * *Rozwiązanie:* Zdiagnozowałem problem z rozwiązywaniem nazw. Ręcznie przypisałem adres IP Kontrolera Domeny jako główny serwer DNS w ustawieniach IPv4 klienta, co natychmiast rozwiązało problem.

## 📸 Zrzuty ekranu
<img width="3429" height="1385" alt="Weryfikacja domeny" src="https://github.com/user-attachments/assets/0136a436-9edb-47c3-af18-aec330d29430" />
<img width="3430" height="1385" alt="OU" src="https://github.com/user-attachments/assets/e0aeee1d-1b56-402b-b6e6-853384b085eb" />
<img width="3431" height="1387" alt="Polityka GPO" src="https://github.com/user-attachments/assets/320a42b6-fbf9-4cd5-baf3-e7350cc6e075" />
<img width="3433" height="1386" alt="Zmapowany dysk" src="https://github.com/user-attachments/assets/6a53eb05-7b52-45d3-9467-cc6379261be4" />
