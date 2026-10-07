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


## Phase 2: Wazuh SIEM & Security Monitoring

W kolejnym etapie rozwoju mojego domowego laba skupiłem się na wdrożeniu warstwy bezpieczeństwa, monitoringu (SOC / Blue Team) oraz automatyzacji powiadomień.

### Wdrożone komponenty i konfiguracja
1. **Wazuh SIEM Manager & Agent:** 
   * Uruchomienie menedżera Wazuh na systemie Ubuntu.
   * Konfiguracja sieci wewnętrznej w VirtualBox (`intnet`) oraz stabilnego routingu i statycznego adresowania IP.
   * Pomyślne podłączenie agenta Wazuh na kontrolerze domeny (`DC01`) i weryfikacja statusu aktywnego.
2. **Monitoring Active Directory:**
   * Konfiguracja zbierania logów z kanału bezpieczeństwa systemu Windows (Security Event Channel).
   * Śledzenie kluczowych zdarzeń w domenie, m.in. tworzenia nowych kont użytkowników oraz modyfikacji ich atrybutów (Event ID `4720`, `4738` i powiązane).
3. **Pipeline powiadomień (Postfix + Mailtrap):**
   * Konfiguracja lokalnego przekaźnika pocztowego Postfix na maszynie Ubuntu.
   * Uruchomienie uwierzytelniania SASL (`smtp_sasl_auth_enable`) oraz zmapowanie danych w pliku `sasl_passwd` w celu spełnienia wymogów bezpieczeństwa zewnętrznej piaskownice SMTP (`sandbox.smtp.mailtrap.io`).
   * Automatyczna dostawa alertów bezpieczeństwa Wazuh bezpośrednio do skrzynki testowej.

### Dowody i zrzuty ekranu (Screenshots)
<img width="1710" height="1387" alt="Stan Wazuh" src="https://github.com/user-attachments/assets/d508fe6c-b876-491b-ab36-866b187f4019" />
<img width="1024" height="830" alt="Logi Wazuh" src="https://github.com/user-attachments/assets/b1a1f409-77ea-43ab-88d7-b3ed810bcd08" />
<img width="1715" height="1386" alt="Logi WS" src="https://github.com/user-attachments/assets/6b0e3602-49d1-4b1e-8f6a-629062351fcd" />
<img width="1024" height="389" alt="MailTrap" src="https://github.com/user-attachments/assets/bd4022b9-0175-4457-ad72-ecba3efd8648" />


