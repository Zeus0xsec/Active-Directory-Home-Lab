# AD Helpdesk Home Lab (Active Directory, DHCP, GPO, SMB)

[🇬🇧 English](README.md) | 🇵🇱 **Polski**

Zwirtualizowane środowisko w stylu firmowym do ćwiczenia codziennej pracy IT Support / Service Desk: administracja użytkownikami i grupami, diagnostyka DHCP i DNS, Group Policy oraz udziały plikowe. Zbudowane w Oracle VirtualBox.

## Architektura

| Maszyna | System | Rola | Adres |
|---|---|---|---|
| DC01 | Windows Server 2022 Standard (Evaluation) | AD DS, DNS, DHCP, udział SMB | 192.168.10.11 (statyczny) |
| Ubuntu LAB | Ubuntu | Menedżer Wazuh, Postfix (zob. [wazuh-siem-homelab](../wazuh-siem-homelab)) | 192.168.10.12 (statyczny) |
| Klienty Win11 | Windows 11 Pro / Enterprise (Evaluation) | Stacje robocze w domenie | DHCP, 192.168.10.20-100 |

```mermaid
flowchart LR
  subgraph NET["Sieć wewnętrzna VirtualBox 192.168.10.0/24"]
    DC["DC01 - Windows Server 2022<br/>AD DS, DNS, DHCP, SMB<br/>192.168.10.11"]
    W["Klienty Windows 11<br/>DHCP 192.168.10.20-100"]
    UB["Ubuntu - Wazuh + Postfix<br/>192.168.10.12"]
  end
  W -- "DHCP, DNS, Kerberos, SMB" --> DC
  DC -- "agent Wazuh + Sysmon" --> UB
```

## Co jest skonfigurowane

- Domena `cyberlab.local` na DC01, dwa klienty Windows 11 dołączone do domeny.
- Struktura OU: `Pracownicy` z jednostkami `Admin`, `HR`, `IT`, `SPRZEDAZ`; oprócz tego `Komputery` i `Uzytkownicy`.
- Zakres DHCP `lab-scope`: 192.168.10.20 - 192.168.10.100 /24, dzierżawa 8 dni. Serwery ze stałymi adresami (.11, .12) są poza zakresem, żeby uniknąć konfliktów IP.
- Group Policy blokujące Wiersz poleceń i Panel sterowania dla pracowników. Sprawdzone przez `gpresult /r` dla użytkownika z OU `SPRZEDAZ`.
- Udział SMB `Dane Firmowe` na DC01, zmapowany jako dysk `Z:` na klientach.
- Zadania w stylu helpdesku: tworzenie użytkowników, reset hasła, włączanie i wyłączanie kont, przenoszenie między OU.

## Dowody

| | |
|---|---|
| ![Dołączenie do domeny](<img width="3430" height="1385" alt="01-domain-join-proof" src="https://github.com/user-attachments/assets/912a21db-40e6-4495-b59e-bfca69ec5dca" />
) **Klient dołączony do `cyberlab.local`** | ![whoami](<img width="3429" height="1385" alt="02-domain-user-whoami" src="https://github.com/user-attachments/assets/c5f245c9-b681-4718-97e1-b541a4ed53fb" />
) **Zalogowany użytkownik domenowy (`whoami`)** |
| ![Struktura OU](<img width="1714" height="1389" alt="03-ou-structure" src="https://github.com/user-attachments/assets/c56028e2-c476-494d-9593-36ae00c6b325" />
) **Struktura OU** | ![GPO](<img width="3431" height="1387" alt="04-gpo-block-cmd" src="https://github.com/user-attachments/assets/f558cf9d-7d82-4a8b-929c-34e63f91e2ed" />
) **GPO podpięte, Wiersz poleceń zablokowany na kliencie** |
| ![gpresult]() **`gpresult /r`: polityka zastosowana dla użytkownika z OU SPRZEDAZ** | ![SMB](<img width="779" height="563" alt="05-gpresult-user-sprzedaz" src="https://github.com/user-attachments/assets/bcadcd0f-905f-4f7c-934b-6e6e3e1dccba" />
) **Udział SMB i zmapowany dysk** |
| ![Zakres DHCP]() **Zakres DHCP** | ![Dzierżawa](<img width="1714" height="1390" alt="07-dhcp-scope" src="https://github.com/user-attachments/assets/a14c0a4a-ff25-43ef-bdff-15b062efbf80" />
) **Dzierżawa klienta z 192.168.10.11 (`ipconfig /all`)** |
| ![Pracownik]() **Logowanie konta pracownika** | |

## Opisy rozwiązanych problemów

Prawdziwe problemy z tego labu zapisane jako runbooki: [helpdesk-runbooks](../helpdesk-runbooks).

## Znane problemy i następne kroki

- Opcja routera w DHCP wskazuje obecnie na DC01. Zamienię ją na prawdziwą bramę (planowany pfSense).
- DC01 rejestruje w DNS także adres z karty NAT, przez co klienci mogą dostać zły IP. Do wyłączenia rejestracji DNS na tej karcie.
- Brak strefy wyszukiwania wstecznego (`nslookup` pokazuje `Server: UnKnown`).
- Licencje Evaluation wygasają (Server 180 dni, Windows 11 Enterprise 90 dni). Trzymam snapshoty i dokumentuję konfigurację, żeby dało się odtworzyć lab.
- Test uprawnień NTFS: zrzut karty Zabezpieczenia i Effective Access do dodania.
