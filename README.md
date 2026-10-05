#  Active Directory & Infrastructure Home Lab

##  O projekcie
Wdrożenie i konfiguracja lokalnego środowiska wirtualnego opartego o Windows Server 2022 oraz Windows 11 Enterprise w celu symulacji infrastruktury firmowej.

##  Użyte Technologie
* Windows Server 2022 (Active Directory DS, DNS, GPO, SMB)
* Windows 11 Pro / Enterprise
* Oracle VirtualBox (Internal Network / Isolated Lab)
* PowerShell / CLI


##  Zrealizowane zadania & Dowody (Screenshots)

1. Konfiguracja AD DS i Dołączenie Klienta
Skonfigurowano kontroler domeny `cyberlab.local`. Stacja robocza Windows 11 została pomyślnie dołączona do domeny.
<img width="3429" height="1385" alt="Weryfikacja domeny" src="https://github.com/user-attachments/assets/26850b53-ecf1-4b10-bf88-d86f76744132" />

2. Struktura OU (Organizational Units)
Zaprojektowano czytelną strukturę OU (`Firma` -> `Uzytkownicy` / `Komputery`) i przeniesiono obiekty domenowe.
<img width="3430" height="1385" alt="OU" src="https://github.com/user-attachments/assets/c810e74a-9f52-4849-8d9b-65e4de69ce7c" />

3. Wdrożenie Polityk GrupRH (GPO)
Utworzono i wyegzekwowano politykę GPO blokującą dostęp do Wiersza Poleceń dla użytkowników domenowych.
<img width="3431" height="1387" alt="Polityka GPO" src="https://github.com/user-attachments/assets/c03358a2-18d3-4d3a-9be1-c9b20bac9df8" />

4. Udziały Plikowe SMB i Uprawnienia NTFS
Skonfigurowano bezpieczny udział plikowy `\\DC01\Dane_Firmowe` oraz zmapowano go automatycznie na stacji roboczej.
<img width="3433" height="1386" alt="Zmapowany dysk" src="https://github.com/user-attachments/assets/34dfffa6-a6e5-42af-a527-bc56ecdcba91" />
