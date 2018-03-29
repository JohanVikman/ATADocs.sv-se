---
title: Referens till Azure ATP SIEM | Microsoft Docs
description: Innehåller exempel på misstänkt aktivitetsloggar som skickas från Azure ATP till din SIEM.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/28/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 0a632473490d157e2b85a30bdb82947982da9551
ms.sourcegitcommit: 7c9fe4eb781bec71129310a6e0c5e76b022a0213
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/28/2018
---
*Gäller för: Azure Advanced Threat Protection*


# <a name="azure-atp-siem-log-reference"></a>Referens till Azure ATP SIEM

Azure ATP kan vidarebefordra misstänkt aktivitet och övervakning notifieringar händelser till din SIEM. Händelser för misstänkta aktiviteter skickas i CEF-format. Den här referensartikeln innehåller exempel på loggar över misstänkt aktivitet som skickas till din SIEM.

## <a name="sample-azure-atp-suspicious-activities-in-cef-format"></a>Exemplet Azure ATP misstänkta aktiviteter i CEF-format
Följande fält och deras värden vidarebefordras till din SIEM-server:

-   start – starttiden för aviseringen
-   suser – kontot (bör vanligtvis vara användarkontot) som aviseringen gäller
-   shost – källdatorn för aviseringen
-   outcome – anger om aktiviteten som utfördes lyckades/misslyckades i aviseringen  
-   msg – en beskrivning av aviseringen
-   cnt – för aviseringar som har ett antal gånger som Avisera har hänt (till exempel brute-force som har en del av att gissa lösenord)
-   app – protokollet som används i aviseringen
-   externalId – händelse-ID Azure ATP skrivs till händelseloggen som motsvarar den här aviseringen
-   CS #label & cs # – dessa är kund-strängar att CEF tillåter för att använda cs #label är namnet på det nya fältet och cs # värde, till exempel: cs1Label = url cs1 =https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

I det här exemplet är cs1 ett fält som innehåller en URL till aviseringen.

## <a name="sample-logs"></a>Exempelloggar

I följande exempel loggar följa RFC 5242, men Azure ATP har också stöd för RFC 3164.

Prioriteter:

- 3=Low
- 5=Medium
- 10 = hög

### <a name="bruteforce--ldap"></a>BruteForce – LDAP
02-21-2018  16:20:21    Auth.Warning    192.168.0.220   1 2018-02-21T14:20:06.156238+00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|LdapBruteForceSecurityAlert|Brute force attack using LDAP simple bind|5|start=2018-02-21T14:19:41.7422810Z app=Ldap suser=Wofford Thurston shost=CLIENT1 msg=A brute force attack using the Ldap protocol was attempted on Wofford Thurston (Software Engineer) from CLIENT1 (100 guess attempts). cnt=100 externalId=2004 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a


### <a name="bruteforce"></a>BruteForce
2018-02-21 16:19:20 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:15.397995 + 00:00 CENTER CEF 6076 BruteForceSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | BruteForceSecurityAlert | Misstänkt autentiseringsfel | 5 | start = 2018-02-21T14:19:03.3831122Z app = Kerberos shost = KLIENT1 ignorerad = misstänkta autentiseringsfel som indikerar en möjlig brute-force attack upptäcktes från KLIENT1. externalId=2023 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6
### <a name="privilege-escalation"></a>Eskalering av privilegier
#### <a name="silver"></a>Silver
2018-02-21 16:19:20 Auth.Error 192.168.0.220 1 2018-02-21T14:19:15.186167 + 00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | ForgedPacSecurityAlert | Privilegiet eskalering med förfalskad auktoriseringsdata | 10 | start = 2018-02-21T14:19:02.8595383Z app = Kerberos suser = Användare1 ignorerad = Användare1 gjordes ett försök att eskalera privilegier till host/domain1.test.local från KLIENT1 med förfalskad auktoriseringsdata. externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/029189e1-6bb4-490b-bcaf-5fac4457e9f3
#### <a name="gold"></a>Guld
2018-02-21 16:19:20 Auth.Error 192.168.0.220 1 2018-02-21T14:19:14.358037 + 00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | ForgedPacSecurityAlert | Privilegiet eskalering med förfalskad auktoriseringsdata | 10 | start = 2018-02-21T14:19:02.8595383Z app = Kerberos suser = Användare1 ignorerad = det gick inte att eskalera privilegier mot DC1 till host/domain1.test.local från KLIENT1 med förfalskad auktoriseringsdata Användare1. externalId=2013 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f3359eff-cb59-44b9-82b6-5e82ff06e6c8
### <a name="golden-ticket"></a>Golden ticket
2018-02-21 16:22:39 Auth.Error 192.168.0.220 1 2018-02-21T14:22:34.274054 + 00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | GoldenTicketSecurityAlert | Kerberos Golden Ticket aktivitet | 10 | start = 2018-02-21T14:19:03.2416152Z app = Kerberos suser = Lanell Campos ignorerad = misstänkt användning av Lanell Campos (programvara tekniker)'s Kerberos-biljett, som indikerar en möjlig Golden Ticket-attack, upptäcktes. externalId=2022 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0
### <a name="honey-token-activity"></a>Honey Token-aktivitet
2018-02-21 16:20:36 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:34.106162 + 00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | HoneytokenActivitySecurityAlert | Honeytoken aktivitet | 5 | start = 2018-02-21T14:20:26.6705617Z app = Kerberos suser = honung ignorerad = följande aktiviteter utfördes av honung: \r\nLogged i till KLIENT2 via DC1. externalId=2014 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c
### <a name="suspicious-replication-of-directory-services"></a>Misstänkt replikering av katalogtjänster
02-21-2018  16:21:22    Auth.Error  192.168.0.220   1 2018-02-21T14:21:13.978554+00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DirectoryServicesReplicationSecurityAlert|Malicious replication of directory services|10|start=2018-02-21T14:19:03.9975656Z app=Drsr shost=CLIENT1 msg=Malicious replication requests were successfully performed by user1, from CLIENT1 against DC1. outcome=Success externalId=2006 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7
### <a name="malicious-data-protection-private-information-request"></a>Skadlig privat informationsbegäran för dataskydd
2018-02-21 16:22:08 Auth.Error 192.168.0.220 1 2018-02-21T14:21:54.080266 + 00:00 CENTER CEF 6076 RetrieveDataProtectionBackupKeyS ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | RetrieveDataProtectionBackupKeySecurityAlert | Skadlig Data Protection privat informationsbegäran | 10 | start = 2018-02-21T14:19:41.8382786Z app = LsaRpc shost = KLIENT1 ignorerad = Användare1 utförs 1 lyckas försöker från KLIENT1 ska hämta DPAPI domän reservnyckel från DC1. externalId=2020 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/b22221d1-764a-4fae-a5ce-e6a0c69dc55a

### <a name="over-pass-the-hash"></a>Over-pass-the-hash
2018-02-21 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Kryptering för nedgradering av aktiviteten | 5 | start = 2018-02-21T14:19:41.8737870Z app = Kerberos ignorerad = krypteringsmetod i fältet Encrypted_Timestamp för AS_REQ meddelande från KLIENT1 har sjunkit baserat på tidigare inlärda beteende. This may be a result of a credential theft using Overpass-the-Hash from CLIENT1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2
### <a name="pass-the-hash"></a>Pass-the-hash
02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheHashSecurityAlert|Identity theft using Pass-the-Hash attack|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (Software Engineer)'s hash was stolen from one of the computers previously logged into by Eugene Jenkins (Software Engineer) and used from CLIENT1. externalId=2017 cs1Label=url cs1=https://test-syslog.eng.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd
### <a name="account-enumeration"></a>Kontouppräkning
2018-02-21 16:19:35 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:27.540731 + 00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | AccountEnumerationSecurityAlert | Rekognosering med kontouppräkning | 5 | start = 2018-02-21T14:19:02.6045416Z app = Kerberos shost = KLIENT1 suser = LMaldonado ignorerad = misstänkt uppräkningen aktiviteten med Kerberos-protokollet som härrör från KLIENT1 observerades och för att gissa Lamon Maldonado (programvara tekniker). externalId=2003 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d
### <a name="dns-recon"></a>DNS-rekognosering
02-21-2018  16:20:06    Auth.Warning    192.168.0.220   1 2018-02-21T14:19:54.063994+00:00 CENTER CEF 6076 DnsReconnaissanceSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|DnsReconnaissanceSecurityAlert|Reconnaissance using DNS|5|start=2018-02-21T14:19:41.9417776Z app=Dns shost=CLIENT1 request=demo query requestMethod=Axfr reason=NoError outcome=Success msg=Suspicious DNS activity was observed, originating from CLIENT1 (which is not a DNS server). Frågan var för demo-fråga (typ Axfr). Svaret var NoError. externalId=2007 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6f69e1e7-304a-4054-8edf-33f26c1f004c


### <a name="smb-session-enumeration"></a>SMB-sessionsuppräkning
2018-02-21 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.962930 + 00:00 CENTER CEF 6076 EnumerateSessionsSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | EnumerateSessionsSecurityAlert | Rekognosering med SMB-Sessionsuppräkningen | 5 | start = 2018-02-21T14:19:03.2071170Z app = SrvSvc shost = KLIENT1 ignorerad = SMB-session uppräkningen försök har utförts User1 från KLIENT1 mot DC1 exponera Eugene Jenkins (användare2-dator) . externalId=2012 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/622c38ab-324f-4c1f-9caa-1fe85db3b440
### <a name="sam-r-enumeration"></a>SAM-R-uppräkning
2018-02-21 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + 00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | SamrReconnaissanceSecurityAlert | Rekognosering med directory services uppräkningen | 5 | start = 2018-02-21T14:19:41.9912772Z app = Samr shost = KLIENT1 suser = Användare1 resultat = lyckade ignorerad = följande katalogtjänsterna uppräkningar protokollet SAMR försökte mot DC1 från Client1:\r\nSuccessful uppräkning av alla grupper i domain1.test.local User1. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="remote-execution"></a>Fjärrkörning
2018-02-21 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + 00:00 CENTER CEF 6076 RemoteExecutionSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | RemoteExecutionSecurityAlert | Fjärrkörning försök upptäckte | 5 | start = 2018-02-21T14:19:41.9912772Z app = Wmi shost = KLIENT1 suser = Användare1 resultat = lyckade ignorerad = följande försök utfördes på DC1 från CLIENT1:\r\nSuccessful fjärrkörning av en eller flera WMI för fjärrkörning metoder som ANVÄNDARE1. externalId=2019 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="skeleton-key"></a>Dyrk
2018-02-21 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Kryptering för nedgradering av aktiviteten | 5 | start = 2018-02-21T14:19:41.8737870Z app = Kerberos ignorerad = krypteringsmetod i fältet ETYPE_INFO2 för KRB_ERR meddelande från KLIENT1 har sjunkit baserat på tidigare inlärda beteende. Detta kan bero på en stommen nyckel på DC1. externalId=2011 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2

### <a name="unusual-protocol-implementation"></a>Onormal protokollimplementering
02-21-2018  16:21:22    Auth.Warning    192.168.0.220   1 2018-02-21T14:21:13.916050+00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|AbnormalProtocolSecurityAlert|Unusual protocol implementation|5|start=2018-02-21T14:19:03.1981155Z app=Ntlm shost=CLIENT2 outcome=Success msg=There were attempts to authenticate from CLIENT2 against DC1 using an unusual protocol implementation. This may be a result of malicious tools used to execute attacks such as Pass-the-Hash and brute force. externalId = 2002 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs1 =https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4

### <a name="malicious-service-creation"></a>Skapa en skadlig tjänst
2018-02-21 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.254930 + 00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | MaliciousServiceCreationSecurityAlert | Skapa misstänkta tjänster | 5 | start = 2018-02-21T14:19:41.7897808Z app = ServiceInstalledEvent shost = KLIENT1 ignorerad = Användare1 skapade MaliciousService för att kunna köra potentiellt skadliga kommandon på KLIENT1. externalId=2026 cs1Label=url cs1=https://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c

### <a name="pass-the-ticket"></a>Pass the Ticket

02-21-2018  17:04:47    Auth.Error  192.168.0.220   1 2018-02-21T15:04:33.537583+00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï»¿0|Microsoft|Azure ATP|2.22.4228.22540|PassTheTicketSecurityAlert|Identity theft using Pass-the-Ticket attack|10|start=2018-02-21T15:02:22.2577465Z app=Kerberos suser=Eugene Jenkins msg=Eugene Jenkins (Software Engineer)'s Kerberos tickets were stolen from Admin-PC to Victom-PC and used to access krbtgt/DOMAIN1.TEST.LOCAL. externalId=2017 cs1Label=url cs1=https://contoso-corp.eng.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd


## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)