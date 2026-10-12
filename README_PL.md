# 🛡️ Active Directory & Infrastructure Home Lab

[![PL](https://img.shields.io/badge/Język-Polski-red.svg)](README_PL.md)
[![EN](https://img.shields.io/badge/Language-English-blue.svg)](README.md)

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
<img width="3429" height="1385" alt="Weryfikacja domeny" src="<img width="3429" height="1385" alt="Weryfikacja domeny" src="https://github.com/user-attachments/assets/f7d08a87-e773-402e-95af-ab9f3ac3fc69" />


2. Struktura OU (Organizational Units)
Zaprojektowano czytelną strukturę OU (`Firma` -> `Uzytkownicy` / `Komputery`) i przeniesiono obiekty domenowe.
<img width="3430" height="1385" alt="OU" src="<img width="3430" height="1385" alt="OU" src="https://github.com/user-attachments/assets/dd9cf7de-0782-4daa-a8d3-879c8e019937" />
   

3. Wdrożenie Polityk GrupRH (GPO)
Utworzono i wyegzekwowano politykę GPO blokującą dostęp do Wiersza Poleceń dla użytkowników domenowych.
<img width="3431" height="1387" alt="Polityka GPO" src="<img width="3431" height="1387" alt="Polityka GPO" src="https://github.com/user-attachments/assets/8e59aeb7-1ced-4f4d-806b-22347f855aac" />
   

4. Udziały Plikowe SMB i Uprawnienia NTFS
Skonfigurowano bezpieczny udział plikowy `\\DC01\Dane_Firmowe` oraz zmapowano go automatycznie na stacji roboczej.
<img width="3433" height="1386" alt="Zmapowany dysk" src="<img width="3433" height="1386" alt="Zmapowany dysk" src="https://github.com/user-attachments/assets/0efadeb1-5c21-432a-b050-178bef8146ed" />
   


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
<img width="1710" height="1387" alt="Stan Wazuh" src="https://github.com/user-attachments/assets/8dff5e7d-bbec-4854-9968-88aadc032fa3" />

<img width="1715" height="1386" alt="Logi WS" src="https://github.com/user-attachments/assets/ae07d906-5dbb-41c6-abdc-6561bffadde5" />

<img width="1024" height="830" alt="Logi Wazuh" src="https://github.com/user-attachments/assets/5d536fdb-a297-47d5-9575-9c035c469b97" />

<img width="1024" height="389" alt="MailTrap" src="https://github.com/user-attachments/assets/92214127-1574-4796-8ca4-22f37368a0e2" />

