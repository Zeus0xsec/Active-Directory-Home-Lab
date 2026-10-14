# 🛡️ Active Directory & Infrastructure Home Lab

[![PL](https://img.shields.io/badge/Język-Polski-red.svg)](README_PL.md)
[![EN](https://img.shields.io/badge/Language-English-blue.svg)](README.md)

##  O projekcie
Wdrożenie i konfiguracja lokalnego środowiska wirtualnego opartego o Windows Server 2022 oraz Windows 11 Enterprise w celu symulacji infrastruktury firmowej.

##  Użyte Technologie
- Windows Server 2022 (Active Directory DS, DNS, GPO, SMB, DHCP)
- Windows 11 Pro / Enterprise
- Oracle VirtualBox (Internal Network / Isolated Lab)
- PowerShell / CLI
- Wazuh SIEM / Sysmon / Postfix / Discord Webhooks


##  Zrealizowane zadania & Dowody (Screenshots)

1. Konfiguracja AD DS i Dołączenie Klienta
Skonfigurowano kontroler domeny `cyberlab.local`. Stacja robocza Windows 11 została pomyślnie dołączona do domeny.
<img width="3429" height="1385" alt="Weryfikacja domeny" src="https://github.com/user-attachments/assets/f7d08a87-e773-402e-95af-ab9f3ac3fc69" />


2. Struktura OU (Organizational Units)
Zaprojektowano czytelną strukturę OU (`Firma` -> `Uzytkownicy` / `Komputery`) i przeniesiono obiekty domenowe.
<img width="3430" height="1385" alt="OU" src="https://github.com/user-attachments/assets/dd9cf7de-0782-4daa-a8d3-879c8e019937" />
   

3. Wdrożenie Polityk GrupRH (GPO)
Utworzono i wyegzekwowano politykę GPO blokującą dostęp do Wiersza Poleceń dla użytkowników domenowych.
<img width="3431" height="1387" alt="Polityka GPO" src="https://github.com/user-attachments/assets/8e59aeb7-1ced-4f4d-806b-22347f855aac" />
   

4. Udziały Plikowe SMB i Uprawnienia NTFS
Skonfigurowano bezpieczny udział plikowy `\\DC01\Dane_Firmowe` oraz zmapowano go automatycznie na stacji roboczej.
<img width="3433" height="1386" alt="Zmapowany dysk" src="https://github.com/user-attachments/assets/0efadeb1-5c21-432a-b050-178bef8146ed" />
   

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


## Phase 3: Architektura Sieciowa, Hardening GPO i Zaawansowany Monitoring

Dzisiaj skupiłem się na wdrożeniu pełnej architektury sieciowej, twardym hardeningu środowiska oraz integracji zaawansowanego rurociągu alertów SOC.

### Wdrożone komponenty i konfiguracja
1. **Usługa DHCP (Windows Server):** 
   * Skonfigurowanie serwera DHCP z zakresem adresów (192.168.10.20–100).
   * Wyznaczenie bezpiecznego bufora dla statycznego IP kontrolera domeny (.11), zapewniając dynamiczną, ale kontrolowaną konfigurację dla maszyn w sieci wewnętrznej.
2. **Nowy klient i infrastruktura domeny:**
   * Podłączenie nowej stacji roboczej (Windows 11 Enterprise), która poprawnie pobrała adresację DHCP oraz wpisy DNS.
   * Pomyślne dołączenie maszyny do domeny `cyberlab.local` i przetestowanie bezpośredniego logowania na utworzone konta pracowników.
3. **Zaawansowana struktura OU i Zarządzanie Tożsamością:**
   * Podział użytkowników w Active Directory na dedykowane jednostki organizacyjne (IT, HR, Sprzedaż, Admini).
   * Zastosowanie i przetestowanie polityk haseł, blokad kont oraz procedur ich resetowania.
4. **Hardening GPO (Group Policy Objects):**
   * Wdrożenie polityki GPO blokującej Panel Sterowania dla zwykłych pracowników.
   * Skuteczne ograniczenie uprawnień na stacjach roboczych i udane testy egzekwowania nałożonych restrykcji.
5. **Zaawansowany monitoring (Sysmon + Wazuh + Discord):**
   * Rozbudowa rurociągu alertów: integracja zdarzeń generowanych przez Sysmon.
   * Skonfigurowanie alertów tak, by reguły o wysokim poziomie krytyczności (level > 8) trafiały błyskawicznie nie tylko do dashboardu Wazuh, ale także jako powiadomienia w czasie rzeczywistym na dedykowany kanał na Discordzie.

### Dowody i zrzuty ekranu (Screenshots)
<img width="1021" height="851" alt="DHCP DOWOD" src="https://github.com/user-attachments/assets/d887da61-3563-4bad-af2b-ac646edd6864" />
<img width="1714" height="1390" alt="DHCP" src="https://github.com/user-attachments/assets/b7c50adb-c8a9-4685-b203-5abbe55de0dd" />
<img width="1017" height="846" alt="PRACOWNIK" src="https://github.com/user-attachments/assets/98089ab7-e6d4-4e9d-baab-2e9692eb9401" />
<img width="1714" height="1389" alt="AD" src="https://github.com/user-attachments/assets/9174dad8-9c84-409a-8872-8cedabc4fa2a" />
<img width="1713" height="1325" alt="SYSMON" src="https://github.com/user-attachments/assets/91239ef7-7f3d-4417-9999-e5947a934b69" />
<img width="1023" height="809" alt="LOGI SYSMON" src="https://github.com/user-attachments/assets/f67caa65-5438-49d1-9c41-a97d39a126b9" />
<img width="2190" height="1273" alt="LOGI DC" src="https://github.com/user-attachments/assets/e1b1ad47-3326-41c2-be5d-d953fc14d697" />

## Faza 4: Utwardzanie GPO, Bezpieczeństwo SMB/NTFS i Monitoring FIM w Czasie Rzeczywistym

W tej fazie skupiłem się na wdrożeniu rygorystycznych polityk bezpieczeństwa w domenie, rozwiązaniu konfliktów uprawnień na udziałach sieciowych oraz włączeniu monitorowania integralności plików (FIM) w czasie rzeczywistym.

### Wdrożone Elementy i Konfiguracja
1. **Utwardzanie GPO RDP i Kontrola Zapory:**
   * Ograniczono dostęp do protokołu Remote Desktop Protocol (RDP / Port 3389) za pomocą GPO (*Przydzielanie praw użytkownika -> Zezwalaj na logowanie przez Usługi pulpitu zdalnego*).
   * Skonfigurowano polityki zezwalające na połączenia pulpitu zdalnego wyłącznie wyznaczonym grupom bezpieczeństwa IT/Admin.
2. **PowerShell ScriptBlock Logging (Event ID 4104):**
   * Wdrożono audytowanie PowerShella w całej domenie za pomocą GPO (`Włącz rejestrowanie bloków skryptów programu PowerShell`).
   * Skonfigurowano rejestrowanie logów w celu przechwytywania pełnej treści skryptów, co umożliwia detekcję zaciemnionych lub zakodowanych poleceń.
3. **Automatyczne Mapowanie Dysków Sieciowych (Item-Level Targeting):**
   * Skonfigurowano mapowanie dysków w GPO, aby automatycznie montować `\\DC01\WspolnydyskIT` jako dysk `Z:`.
   * Zastosowano Item-Level Targeting, aby dysk mapował się wyłącznie dla uprawnionych grup użytkowników w domenie.
4. **Synchronizacja Uprawnień SMB Share i NTFS:**
   * Rozwiązano problemy z tworzeniem plików oraz dziedziczeniem praw poprzez zsynchronizowanie uprawnień udziału SMB i zabezpieczeń NTFS.
   * Wykorzystano narzędzia CLI (`icacls` oraz `Grant-SmbShareAccess`) do nadania pełnej kontroli (`(OI)(CI)F`) z zachowaniem dziedziczenia dla obiektów i kontenerów.
5. **Wazuh File Integrity Monitoring (FIM / Syscheck):**
   * Skonfigurowano plik `ossec.conf` na `DC01` pod kątem monitorowania folderu `C:\WspolnydyskIT` w czasie rzeczywistym (`realtime="yes"` oraz `report_changes="yes"`).
   * Zweryfikowano natychmiastowe generowanie alertów SIEM przy zdarzeniach utworzenia pliku, modyfikacji jego zawartości oraz usunięcia.

### Dowody i Zrzuty Ekranu
<img width="1024" height="827" alt="3" src="https://github.com/user-attachments/assets/9849818b-0492-4e2d-b20e-366f8104e6ba" />
<img width="1023" height="832" alt="4" src="https://github.com/user-attachments/assets/56c85d85-d772-46ab-aea2-04119d8e2cd2" />
<img width="2193" height="1122" alt="wspolnydysk" src="https://github.com/user-attachments/assets/57043e52-6d25-40dc-bb7a-b4c7c87a9f87" />
<img width="1715" height="1386" alt="testdysk" src="https://github.com/user-attachments/assets/aa2901df-7259-46f0-8727-540fe5a85756" />
<img width="1634" height="753" alt="testdyskwazuh" src="https://github.com/user-attachments/assets/b9a5c24b-b568-4b04-887b-5782a80269f9" />
<img width="1440" height="846" alt="wspolnydyskwin11" src="https://github.com/user-attachments/assets/a40351d4-d0c2-46b4-b758-0c133dac134f" />






