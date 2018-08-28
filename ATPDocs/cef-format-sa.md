---
title: 'Referens: loggar Azure ATP-SIEM | Microsoft Docs'
description: Innehåller exempel av misstänkt aktivitetsloggar som skickas från Azure ATP till din SIEM.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/20/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 3261155c-3c72-4327-ba29-c113c63a4e6d
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 88056e1dd7523b77569241ccbe3a967c4b7a26ef
ms.sourcegitcommit: 56886d06abd25035ffc9885c69aca9b0ebf14abc
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2018
ms.locfileid: "43039063"
---
*Gäller för: Azure Avancerat skydd*


# <a name="azure-atp-siem-log-reference"></a>Referens: loggar Azure ATP-SIEM

Azure ATP kan vidarebefordra misstänkta aktiviteter och övervakningsaviseringar händelser till din SIEM. Händelser för misstänkta aktiviteter skickas i CEF-format. Den här referensartikeln innehåller exempel på loggar över misstänkt aktivitet som skickas till din SIEM.

## <a name="sample-azure-atp-suspicious-activities-in-cef-format"></a>Exemplet Azure ATP misstänkta aktiviteter i CEF-format
Följande fält och deras värden vidarebefordras till din SIEM-server:

-   start – starttiden för aviseringen
-   suser – kontot (bör vanligtvis vara användarkontot) som aviseringen gäller
-   shost – källdatorn för aviseringen
-   Slutresultat – för aviseringar där det finns en lyckades/misslyckades för den aktivitet som utförs i den här aviseringen  
-   msg – en beskrivning av aviseringen
-   cnt – anger som har ett antal gånger som varnar inträffade (till exempel råstyrkeattacker som har en antalet gissade lösenord)
-   app – protokollet som används i aviseringen
-   externalId – händelse-ID: T Azure ATP skriver till händelseloggen som motsvarar den här aviseringen
-   CS #label & cs # – dessa är kundsträngarna som CEF tillåter för att använda, cs #label är namnet på det nya fältet och cs # är värdet, till exempel: cs1Label = url cs1 =https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

I det här exemplet är cs1 ett fält som innehåller en URL till aviseringen.

## <a name="sample-logs"></a>Exempelloggar

I följande exempel loggar uppfyller RFC 5242, men Azure ATP stöder också RFC 3164.

Prioriteter:

- 3 = låg
- 5 = medium
- 10 = hög

### <a name="bruteforce--ldap"></a>BruteForce – LDAP
2018-02-21 16:20:21 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:06.156238 + 00:00 CENTER CEF 6076 LdapBruteForceSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | LdapBruteForceSecurityAlert | Råstyrkeattack med enkel LDAP-bindning | 5 | start = 2018-02-21T14:19:41.7422810Z app = Ldap suser = Wofford Thurston shost = KLIENT1 msg = en råstyrkeattack med Ldap protokollet försöktes på Wofford Thurston (programvaruutvecklare) från KLIENT1 (100 gissning Försök). cnt = 100 externalId = 2004 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/57b8ac96-7907-4971-9b27-ec77ad8c029a


### <a name="bruteforce"></a>BruteForce
2018-02-21 16:19:20 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:15.397995 + 00:00 CENTER CEF 6076 BruteForceSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | BruteForceSecurityAlert | Misstänkta autentiseringsfel | 5 | start = 2018-02-21T14:19:03.3831122Z app = Kerberos shost = KLIENT1 msg = misstänkta autentiseringsfel som indikerar en möjlig brute force-attack upptäcktes från KLIENT1. externalId = 2023 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/fea88fc7-4110-454d-816d-349032474fd6
### <a name="privilege-escalation"></a>Eskalering av privilegier
#### <a name="silver"></a>Silver
2018-02-21 16:19:20 Auth.Error 192.168.0.220 1 2018-02-21T14:19:15.186167 + 00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | ForgedPacSecurityAlert | Behörighetseskalering med förfalskade auktoriseringsdata | 10 | start = 2018-02-21T14:19:02.8595383Z app = Kerberos suser = user1 msg = user1 försökte eskalera privilegierna host/domain1.test.local från KLIENT1 med hjälp av förfalskade auktoriseringsdata. externalId = 2013 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/029189e1-6bb4-490b-bcaf-5fac4457e9f3
#### <a name="gold"></a>Guld
2018-02-21 16:19:20 Auth.Error 192.168.0.220 1 2018-02-21T14:19:14.358037 + 00:00 CENTER CEF 6076 ForgedPacSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | ForgedPacSecurityAlert | Behörighetseskalering med förfalskade auktoriseringsdata | 10 | start = 2018-02-21T14:19:02.8595383Z app = Kerberos suser = user1 msg = user1 lyckades inte eskalera privilegier mot DC1 till host/domain1.test.local från KLIENT1 med hjälp av förfalskade auktoriseringsdata. externalId = 2013 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/f3359eff-cb59-44b9-82b6-5e82ff06e6c8
### <a name="golden-ticket"></a>Golden ticket
2018-02-21 16:22:39 Auth.Error 192.168.0.220 1 2018-02-21T14:22:34.274054 + 00:00 CENTER CEF 6076 GoldenTicketSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | GoldenTicketSecurityAlert | Kerberos Golden Ticket-aktivitet | 10 | start = 2018-02-21T14:19:03.2416152Z app = Kerberos suser = Lanell Campos msg = misstänkt användning av Lanell Campos (programvaruutvecklare)'s Kerberos-biljett, som indikerar en möjlig gyllene biljett-attack, har identifierats. externalId = 2022 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/702c836e-6f49-4479-9892-80e8bccbfac0
### <a name="kerberos-golden-ticket-nonexistent-account"></a>Kerberos Golden Ticket icke-befintligt konto
2018-01-07 14:28:49 Auth.Error 192.168.0.100 1 2018-07-01T11:28:35.546638 + 00:00 CENTER CEF 38768 ForgedPrincipalSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.39.0.0 | ForgedPrincipalSecurityAlert | Guld för Kerberos-biljett - konto | 10 | start = 2018-07-01T09:48:31.2567987Z app = Kerberos suser=domain1.test.local\fake msg=domain1.test.local\fake som inte finns i Active Directory, används en Kerberos-biljett. Biljetten har upptäckts från 2-datorer till 3 resurser. Detta kan tyda på en möjlig gyllene biljett-attack. externalId = 2027 cs1Label = url cs1 =https://contoso-corp.atp.azure.com:13000/securityAlert/98f050d4-9134-429c-8e54-d8eeb19849c4


### <a name="honey-token-activity"></a>Honey Token-aktivitet
2018-02-21 16:20:36 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:34.106162 + 00:00 CENTER CEF 6076 HoneytokenActivitySecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | HoneytokenActivitySecurityAlert | Honeytoken-aktivitet | 5 | start = 2018-02-21T14:20:26.6705617Z app = Kerberos suser = honung msg = följande aktiviteter utfördes av honung: \r\nLogged i att KLIENT2 via DC1. externalId = 2014 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/9249fe9a-c883-46dd-a4da-2a1fca5f211c
### <a name="suspicious-replication-of-directory-services"></a>Misstänkt replikering av katalogtjänster
2018-02-21 16:21:22 Auth.Error 192.168.0.220 1 2018-02-21T14:21:13.978554 + 00:00 CENTER CEF 6076 DirectoryServicesReplicationSecu ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | DirectoryServicesReplicationSecurityAlert | Skadlig replikering av katalogtjänster | 10 | start = 2018-02-21T14:19:03.9975656Z app = Drsr shost = KLIENT1 msg = skadlig replikering begäranden utfördes av Användare1, från KLIENT1 mot DC1. resultatet = lyckades externalId = 2006 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/cb95648e-1b6f-4d3b-81b9-7605532787d7
### <a name="suspicious-replication-request-potential-dcshadow-attack"></a>Misstänkt replikeringsbegäran (möjlig DcShadow attack)
07-12-2018 11:18:37 Auth.Error 192.168.0.200 1 2018-07-12T08:18:32.265989 + 00:00 DC1 CEF 3868 DirectoryServicesRogueReplicatio ï» ¿0 | Microsoft | Azure ATP | 2.40.0.0 | DirectoryServicesRogueReplicationSecurityAlert | **Misstänkta replikeringsbegäran (möjlig DcShadow attack)**| 10 | start = 2018-07-12T08:17:55.3816102Z **app = replikering aktivitet** shost = KLIENT1 msg = KLIENT1 som inte är en giltig domän Controller i domain1.test.local, skickas ändringar till katalogobjekt på DC1. externalId = 2029 cs1Label = url cs1 =https://contoso-corp.atp.azure.com:13000/securityAlert/1d5d1444-12cf-4db9-be48-39ebc2f51515
### <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>Misstänkt befordran av domänkontrollant (möjlig DcShadow attack)
07-12-2018 11:18:07 Auth.Error 192.168.0.200 1 2018-07-12T08:18:06.883880 + 00:00 DC1 CEF 3868 DirectoryServicesRoguePromotionS ï» ¿0 | Microsoft | Azure ATP | 2.40.0.0 | DirectoryServicesRoguePromotionSecurityAlert | **Misstänkta befordran av domänkontrollant (möjlig DcShadow attack)**| 10 | start = 2018-07-12T08:17:55.4067092Z app = Ldap shost = KLIENT1 msg = KLIENT1 är en dator i domain1.test.local, registreras som en domänkontrollant på DC1. externalId = 2028 cs1Label = url cs1 =https://contoso-corp.atp.azure.com:13000/securityAlert/97c59b43-dc18-44ee-9826-8fd5d03bd53

### <a name="malicious-data-protection-private-information-request"></a>Skadlig privat informationsbegäran för dataskydd
2018-02-21 16:22:08 Auth.Error 192.168.0.220 1 2018-02-21T14:21:54.080266 + 00:00 CENTER CEF 6076 RetrieveDataProtectionBackupKeyS ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | RetrieveDataProtectionBackupKeySecurityAlert | Skadliga Data Protection privat informationsbegäran | 10 | start = 2018-02-21T14:19:41.8382786Z app = LsaRpc shost = KLIENT1 msg = user1 utförs 1 lyckade försök från KLIENT1 att hämta DPAPI-domänens säkerhetskopieringsnyckel från DC1. externalId = 2020 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/b22221d1-764a-4fae-a5ce-e6a0c69dc55a

### <a name="over-pass-the-hash"></a>Over-pass-the-hash
2018-02-21 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Krypteringsnedgraderingsaktivitet | 5 | start = 2018-02-21T14:19:41.8737870Z app = Kerberos msg = krypteringsmetod för fältet encrypted_timestamp av AS_REQ meddelande från KLIENT1 har sjunkit baserat på tidigare inlärda beteende. This may be a result of a credential theft using Overpass-the-Hash from CLIENT1. externalId = 2011 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2
### <a name="pass-the-hash"></a>Pass-the-hash
2018-02-21 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583 + 00:00 CENTER CEF 6076 PassTheHashSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | PassTheHashSecurityAlert | Identitetsstöld med Pass-the-Hash-attack | 10 | start = 2018-02-21T15:02:22.2577465Z app = Kerberos suser = Eugene Jenkins msg = Eugene Jenkins (programvaruutvecklare)'s hash stals från en av de datorer som tidigare har loggat in Eugene Jenkins (programvara Engineer) och användes från KLIENT1. externalId = 2017 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd
### <a name="account-enumeration"></a>Kontouppräkning
2018-02-21 16:19:35 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:27.540731 + 00:00 CENTER CEF 6076 AccountEnumerationSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | AccountEnumerationSecurityAlert | Rekognosering med kontouppräkning | 5 | start = 2018-02-21T14:19:02.6045416Z app = Kerberos shost = KLIENT1 suser = LMaldonado msg = misstänkt kontouppräkningsaktivitet med Kerberos-protokollet, som kommer från KLIENT1 observerades och lyckades gissa Lamon Maldonado (programvaruutvecklare). externalId = 2003 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/eb6a35da-ff7f-4ab5-a1b5-a07529a89e6d
### <a name="dns-recon"></a>DNS-rekognosering
2018-02-21 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.063994 + 00:00 CENTER CEF 6076 DnsReconnaissanceSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | DnsReconnaissanceSecurityAlert | Rekognosering med DNS | 5 | start = 2018-02-21T14:19:41.9417776Z app = Dns shost = KLIENT1 begäran = demo fråga requestMethod = Axfr orsak = NoError resultatet = lyckades msg = misstänkt DNS aktivitet observerades från KLIENT1 (som inte är en DNS-server). Frågan var för demo-fråga (Axfr-typ). Svaret var NoError. externalId = 2007 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/6f69e1e7-304a-4054-8edf-33f26c1f004c


### <a name="smb-session-enumeration"></a>SMB-sessionsuppräkning
2018-02-21 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.962930 + 00:00 CENTER CEF 6076 EnumerateSessionsSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | EnumerateSessionsSecurityAlert | Rekognosering med SMB-Sessionsuppräkning | 5 | start = 2018-02-21T14:19:03.2071170Z app = SrvSvc shost = KLIENT1 msg = SMB-session uppräkning försök utfördes av Användare1, från KLIENT1 mot DC1 exponera Eugene Jenkins (användare2-dator) . externalId = 2012 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/622c38ab-324f-4c1f-9caa-1fe85db3b440
### <a name="sam-r-enumeration"></a>Uppräkning av SAM-R
2018-02-21 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + 00:00 CENTER CEF 6076 SamrReconnaissanceSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | SamrReconnaissanceSecurityAlert | Rekognosering med uppräkning av katalogtjänster | 5 | start = 2018-02-21T14:19:41.9912772Z app = Samr shost = KLIENT1 suser = user1 resultatet = lyckades msg = följande katalogtjänsterna uppräkningar med SAMR-protokollet försöktes mot DC1 från Client1:\r\nSuccessful uppräkning av alla grupper i domain1.test.local User1. externalId = 2019 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="remote-execution"></a>Fjärrkörning
2018-02-21 16:22:08 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:54.267658 + 00:00 CENTER CEF 6076 RemoteExecutionSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | RemoteExecutionSecurityAlert | Försök till fjärrkörning har identifierats | 5 | start = 2018-02-21T14:19:41.9912772Z app = Wmi shost = KLIENT1 suser = user1 resultatet = lyckades msg = följande fjärr körningen försök utfördes på DC1 från CLIENT1:\r\nSuccessful fjärrkörning av en eller flera WMI metoder som User1. externalId = 2019 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/f295029a-ffae-408b-9dd0-55424c81eac0
### <a name="skeleton-key"></a>Dyrk
2018-02-21 16:21:07 Auth.Warning 192.168.0.220 1 2018-02-21T14:20:54.145833 + 00:00 CENTER CEF 6076 EncryptionDowngradeSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | EncryptionDowngradeSecurityAlert | Krypteringsnedgraderingsaktivitet | 5 | start = 2018-02-21T14:19:41.8737870Z app = Kerberos msg = krypteringsmetod i fältet ETYPE_INFO2 för KRB_ERR meddelande från KLIENT1 har sjunkit baserat på tidigare inlärda beteende. Detta kan vara ett resultat av en huvudnyckel på DC1. externalId = 2011 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/6354b9ed-6a39-4f5b-b10e-f51bbee879d2

### <a name="unusual-protocol-implementation"></a>Onormal protokollimplementering
2018-02-21 16:21:22 Auth.Warning 192.168.0.220 1 2018-02-21T14:21:13.916050 + 00:00 CENTER CEF 6076 AbnormalProtocolSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | AbnormalProtocolSecurityAlert | Onormal protokollimplementering | 5 | start = 2018-02-21T14:19:03.1981155Z app = Ntlm shost = KLIENT2 resultatet = lyckades msg = det var försök att autentisera från KLIENT2 mot DC1 med hjälp av en ovanlig protokollimplementering. This may be a result of malicious tools used to execute attacks such as Pass-the-Hash and brute force. externalId = 2002 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/40fe98dd-aa42-4540-9d73-831486fdd1e4 cs1 =https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4

### <a name="malicious-service-creation"></a>Skapa skadliga tjänster
2018-02-21 16:20:06 Auth.Warning 192.168.0.220 1 2018-02-21T14:19:54.254930 + 00:00 CENTER CEF 6076 MaliciousServiceCreationSecurity ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | MaliciousServiceCreationSecurityAlert | Misstänkt skapande av tjänst | 5 | start = 2018-02-21T14:19:41.7897808Z app = ServiceInstalledEvent shost = KLIENT1 msg = user1 skapade MaliciousService för att kunna köra potentiellt skadliga kommandon på KLIENT1. externalId = 2026 cs1Label = url cs1 =https://contoso-corp.atp.azure.com/securityAlert/179229b6-b791-4895-b5aa-fdf3747a325c

### <a name="pass-the-ticket"></a>Pass the Ticket
2018-02-21 17:04:47 Auth.Error 192.168.0.220 1 2018-02-21T15:04:33.537583 + 00:00 CENTER CEF 6076 PassTheTicketSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.22.4228.22540 | PassTheTicketSecurityAlert | Identitetsstöld med Pass-the-Ticket-attack | 10 | start = 2018-02-21T15:02:22.2577465Z app = Kerberos suser = Eugene Jenkins msg = Eugene Jenkins (programvaruutvecklare)'s Kerberos biljetter har stals från Admin-PC till Victim-PC och används för att komma åt krbtgt/domän1. TEST. LOKALA. externalId = 2017 cs1Label = url cs1 =https://contoso-corp.eng.atp.azure.com/securityAlert/511f1487-2915-477d-be2e-04cfba702ccd

### <a name="suspicious-vpn-connection"></a>Misstänkt VPN-anslutning
2018-03-07 13:13:12 Auth.Warning 192.168.0.200 1 2018-07-03T10:13:06.187834 + 00:00 DC1 CEF 2520 AbnormalVpnSecurityAlert ï» ¿0 | Microsoft | Azure ATP | 2.39.0.0 | AbnormalVpnSecurityAlert | Misstänkt VPN-anslutning | 5 | start = 2018-06-30T15:34:05.3887333Z app = VpnConnection suser = user1 msg = user1 som är anslutna till en VPN-anslutning med hjälp av 3 datorer från 3 platser.     externalId = 2025 cs1Label = url cs1 =https://contoso-corp.eng.atp.azure.com:13000/securityAlert/88c46b0e-372f-4c06-9935-67bd512c4f68


## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)