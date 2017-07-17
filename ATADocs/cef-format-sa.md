---
title: "Referens: Loggar från ATA till SIEM | Microsoft Docs"
description: "Innehåller exempel på loggar över misstänkta aktiviteter som skickas från ATA till din SIEM-server."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/21/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 601b48ba-a327-4aff-a1f9-2377a2bb7a42
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: ca460647fbed07820e8d19083d5aca19a05bc0a8
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/30/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*


# Referens: Loggar från ATA till SIEM
<a id="ata-siem-log-reference" class="xliff"></a>

ATA kan vidarebefordra händelser för misstänkta aktiviteter och övervakningsaviseringar till din SIEM-server. Händelser för misstänkta aktiviteter skickas i CEF-format. Den här referensartikeln innehåller exempel på loggar över misstänkt aktivitet som skickas till din SIEM.

## Exempel på misstänkta aktiviteter i ATA i CEF-format
<a id="sample-ata-suspicious-activities-in-cef-format" class="xliff"></a>
Följande fält och deras värden vidarebefordras till din SIEM-server:

-   start – starttiden för aviseringen
-   suser – kontot (bör vanligtvis vara användarkontot) som aviseringen gäller
-   shost – källdatorn för aviseringen
-   outcome – anger om aktiviteten som utfördes lyckades/misslyckades i aviseringen  
-   msg – en beskrivning av aviseringen
-   cnt – anger antalet gånger som aviseringen inträffade (till exempel antalet gissade lösenord vid råstyrkeattacker)
-   app – protokollet som används i aviseringen
-   externalId – händelse-ID:t som ATA skriver till händelseloggen för aviseringen
-   cs#label & cs# – det här är kundsträngarna som CEF tillåter; cs#label är namnet på det nya fältet och cs# är värdet, t.ex.: cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa

I det här exemplet är cs1 ett fält som innehåller en URL till aviseringen.

## Exempelloggar
<a id="sample-logs" class="xliff"></a>

Priorities: 3=Low 5=Medium 10=High

### BruteForce – LDAP
<a id="bruteforce--ldap" class="xliff"></a>
05-03-2017          13:35:01               Auth.Warning    192.168.0.220     May  3 10:35:01 CENTER ATA:CEF:0|Microsoft|ATA|.5942.64854|BruteForceSuspiciousActivity|Brute force attack using LDAP simple bind|5|start=2017-05-03T10:34:57.2785534Z app=Ldap suser=Darris Woods shost=CLIENT1 msg=A brute force attack using the Ldap protocol was attempted on Darris Woods (Software Engineer) from CLIENT1 (76 guess attempts). cnt=76 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     May  3 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|Brute force attack using LDAP simple bind|5|start=2017-05-03T10:34:58.7004159Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=A brute force attack using the Ldap protocol was attempted on Dino Hopkins (Software Engineer) from CLIENT1 (3 guess attempts). cnt=3 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70

05-03-2017          13:35:05               Auth.Warning    192.168.0.220     May  3 10:35:05 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|BruteForceSuspiciousActivity|Brute force attack using LDAP simple bind|5|start=2017-05-03T10:34:59.7269332Z app=Ldap suser=Dino Hopkins shost=CLIENT1 msg=A successful brute force attack using the Ldap protocol was attempted on Dino Hopkins (Software Engineer) from CLIENT1 (77 guess attempts). cnt=77 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b2458ca1ec04d05e6a70
### BruteForce
<a id="bruteforce" class="xliff"></a>
05-14-2017          13:27:05               Auth.Warning    192.168.0.220     1 2017-05- ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|BruteForceSuspiciousActivity|Suspicious authentication failures|5|start=2017-05-14T10:27:04.3904739Z app=Kerberos shost=CLIENT1 msg=Suspicious authentication failures indicating a potential brute-force attack were detected from CLIENT1. externalId=2023 cs1Label=url cs1=https://center/suspiciousActivity/591830f98ca1ec11d0c0d7f5
### Eskalering av privilegier
<a id="privilege-escalation" class="xliff"></a>
#### Silver
<a id="silver" class="xliff"></a>
05-10-2017          17:14:15               Auth.Error           192.168.0.220     1 2017-05-10T14:14:15.589415+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Privilege escalation using forged authorization data|10|start=2017-05-10T14:11:51.8053059Z app=Kerberos suser=user1 msg=user1 attempted to escalate privileges to HOST/client1 from CLIENT2 by using forged authorization data. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/591320378ca1ec02543e4747
#### Guld
<a id="gold" class="xliff"></a>
05-10-2017          17:13:30               Auth.Error           192.168.0.220     1 2017-05-10T14:13:30.244377+00:00 CENTER ATA 596 ForgedPacSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|ForgedPacSuspiciousActivity|Privilege escalation using forged authorization data|10|start=2017-05-10T14:11:27.6455273Z app=Kerberos suser=user1 msg=user1 attempted to escalate privileges against DC4 from CLIENT1 by using forged authorization data. externalId=2013 cs1Label=url cs1=https://center/suspiciousActivity/5913200a8ca1ec02543e3ea8
### Golden ticket
<a id="golden-ticket" class="xliff"></a>
05-14-2017          15:57:10               Auth.Warning    192.168.0.220     1 2017-05-14T12:57:10.392730+00:00 CENTER ATA 4732 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Encryption downgrade activity|5|start=2017-05-14T12:55:08.6913033Z app=Kerberos msg=The encryption method of the TGT field of TGS_REQ message from CLIENT1 has been downgraded based on previously learned behavior. This may be a result of a Golden Ticket in-use on CLIENT1. externalId=2009 cs1Label=url cs1=https://center/suspiciousActivity/591854268ca1ec127ceec396
### Honey Token-aktivitet
<a id="honey-token-activity" class="xliff"></a>
05-11-2017          16:49:10               Auth.Warning    192.168.0.220     1 2017-05-11T13:49:10.725605+00:00 CENTER ATA 876 HoneytokenActivitySuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|HoneytokenActivitySuspiciousActivity|Honeytoken activity|5|start=2017-05-11T13:49:09.6455794Z app=Kerberos suser=privtriservice msg=The following activities were performed by privtriservice:\r\nAuthenticated from DC1 using NTLM against corporate resources via DC1. externalId=2014 cs1Label=url cs1=https://center/suspiciousActivity/59146bd68ca1ec036ce57d29
### Misstänkt replikering av katalogtjänster
<a id="suspicious-replication-of-directory-services" class="xliff"></a>
May  3 11:02:28 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DirectoryServicesReplicationSuspiciousActivity|Malicious replication of directory services|10|start=2017-05-03T11:00:13.6560919Z suser=user1 shost=CLIENT1 outcome=Failure msg=Malicious replication requests were attempted by user1, from CLIENT1 against DC1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909b8c48ca1ec04d05ed28d
### Skadlig privat informationsbegäran för dataskydd
<a id="malicious-data-protection-private-information-request" class="xliff"></a>
May  3 13:39:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RetrieveDataProtectionBackupKeySuspiciousActivity|Malicious Data Protection Private Information Request|10|start=2017-05-03T13:37:06.4039886Z app=LsaRpc shost=CLIENT1 suser= outcome=Success msg=An unknown user performed 4 successful attempts from CLIENT1 to retrieve DPAPI domain backup key from DC1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dd868ca1ec04d05fb01d
### Massiv objektborttagning
<a id="massive-object-deletion" class="xliff"></a>
05-14-2017          14:38:34               Auth.Warning    192.168.0.220     1 2017-05-14T11:38:34.898810+00:00 CENTER ATA 3748 MassiveObjectDeletionSuspiciousA ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|MassiveObjectDeletionSuspiciousActivity|Massive object deletion|5|start=2017-05-14T11:33:32.0000000Z msg=496 objects (9.75% of total AD objects) were deleted over a period of no time from domain domain1.test.local. cnt=496 externalId=2016 cs1Label=url cs1=https://center/suspiciousActivity/591841ba8ca1ec0ea4ad587a
### Over-pass-the-hash
<a id="over-pass-the-hash" class="xliff"></a>
05-14-2017          12:07:46               Auth.Warning    192.168.0.220     1 2017-05-14T09:07:46.652319+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Encryption downgrade activity|5|start=2017-05-14T09:07:44.9933773Z app=Kerberos msg=The encryption method of the Encrypted_Timestamp field of AS_REQ message from CLIENT1 has been downgraded based on previously learned behavior. This may be a result of a credential theft using Overpass-the-Hash from CLIENT1. externalId=2010 cs1Label=url cs1=https://center/suspiciousActivity/59181e628ca1ec045cdfa929
### Pass-the-hash
<a id="pass-the-hash" class="xliff"></a>
05-10-2017          17:48:51               Auth.Error           192.168.0.220     1 2017-05-10T14:48:51.998620+00:00 CENTER ATA 596 PassTheHashSuspiciousActivity ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|PassTheHashSuspiciousActivity|Identity theft using Pass-the-Hash attack|10|start=2017-05-10T14:46:50.9463800Z app=Ntlm suser=user2 msg=user2's hash was stolen from one of the computers previously logged into by user2 and used from CLIENT1. externalId=2017 cs1Label=url cs1=https://center/suspiciousActivity/591328538ca1ec02543f9a1a
### Kontouppräkning
<a id="account-enumeration" class="xliff"></a>
05-10-2017          16:44:22               Auth.Warning    192.168.0.220     1 2017-05-10T13:44:22.706381+00:00 CENTER ATA 596 AccountEnumerationSuspiciousActi ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|AccountEnumerationSuspiciousActivity|Reconnaissance using account enumeration|5|start=2017-05-10T13:44:20.9930644Z app=Kerberos shost=CLIENT3 msg=Suspicious account enumeration activity using Kerberos protocol, originating from CLIENT3, was detected. The attacker performed a total of 72 guess attempts for account names, 2 guess attempts matched existing account names in Active Directory. externalId=2003 cs1Label=url cs1=https://center/suspiciousActivity/591319368ca1ec02543c56ee
### DNS-rekognosering
<a id="dns-recon" class="xliff"></a>
05-03-2017          13:16:57               Auth.Warning    192.168.0.220     May  3 10:16:57 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Reconnaissance using DNS|5|start=2017-05-03T10:16:41.8297467Z app=Dns shost=CLIENT1 msg=Suspicious DNS activity was observed, originating from CLIENT1 (which is not a DNS server) against DC1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa 05-03-2017          13:24:21               Auth.Warning    192.168.0.220     May  3 10:24:21 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|DnsReconnaissanceSuspiciousActivity|Reconnaissance using DNS|5|start=2017-05-03T10:24:08.0950753Z app=Dns shost=CLIENT1 request=contoso.com requestMethod=Axfr reason=NameError outcome=Failure msg=Suspicious DNS activity was observed, originating from CLIENT1 (which is not a DNS server). The query was for contoso.com (type Axfr). The response was NameError. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909ae198ca1ec04d05e65fa
### SMB-sessionsuppräkning
<a id="smb-session-enumeration" class="xliff"></a>
May  3 11:55:43 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|EnumerateSessionsSuspiciousActivity|Reconnaissance using SMB Session Enumeration|5|start=2017-05-03T11:52:02.4360718Z app=SrvSvc shost=CLIENT1 msg=SMB session enumeration attempts were successfully performed from CLIENT1 against DC1, exposing user1 (daf::1). cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c53f8ca1ec04d05f1cf1
### SAMR-uppräkning
<a id="samr-enumeration" class="xliff"></a>
May  3 11:44:48 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|SamrReconnaissanceSuspiciousActivity|Reconnaissance using directory services enumeration|5|start=2017-05-03T11:42:46.5911225Z app=Samr shost=CLIENT1 suser=user1 outcome=Success msg=The following directory services enumerations using SAMR protocol were attempted against DC1 from CLIENT1:\r\nSuccessful enumeration of all groups in domain1.test.local by user1 cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909c2b08ca1ec04d05f0e19
### Fjärrkörning
<a id="remote-execution" class="xliff"></a>
May  3 12:36:47 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|RemoteExecutionSuspiciousActivity|Remote execution attempt detected|3|start=2017-05-03T12:34:32.3714348Z app=ServiceControl shost=CLIENT1 suser=Administrator outcome=Success msg=The following remote execution attempts were performed on DC1 from CLIENT1:\r\nSuccessful remote creation of PSEXESVC by Administrator. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cedf8ca1ec04d05f5692
### Dyrk
<a id="skeleton-key" class="xliff"></a>
05-14-2017          12:13:12               Auth.Warning    192.168.0.220     1 2017-05-14T09:13:12.102468+00:00 CENTER ATA 1116 EncryptionDowngradeSuspiciousAct ï»¿CEF:0|Microsoft|ATA|1.8.6455.41882|EncryptionDowngradeSuspiciousActivity|Encryption downgrade activity|5|start=2017-05-14T09:13:03.3509467Z app=Kerberos msg=The encryption method of the ETYPE_INFO2 field of KRB_ERR message from CLIENT2 has been downgraded based on previously learned behavior. This may be a result of a Skeleton Key on DC3. externalId=2011 cs1Label=url cs1=https://center/suspiciousActivity/59181fa88ca1ec045cdfe630
### Onormal protokollimplementering
<a id="unusual-protocol-implementation" class="xliff"></a>
May  3 12:28:19 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|AbnormalProtocolSuspiciousActivity|Unusual protocol implementation|5|start=2017-05-03T12:28:05.3561302Z app=Ntlm shost=CLIENT1 suser=Administrator outcome=Success msg=Administrator successfully authenticated from CLIENT1 against DC1 using an unusual protocol implementation. This may be a result of malicious tools used to execute attacks such as Pass-the-Hash and brute force. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909cce38ca1ec04d05f4ab4
### Känsliga kontoautentiseringsuppgifter har exponerats
<a id="sensitive-account-credentials-exposed" class="xliff"></a>
May  3 13:23:18 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|LdapSimpleBindCleartextPasswordSuspiciousActivity|Sensitive account credentials exposed|3|start=2017-05-03T13:23:09.7798589Z app=Ldap shost=CLIENT1 suser=Administrator msg=Administrator's credentials were exposed in clear text using LDAP simple bind from CLIENT1. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909d9c68ca1ec04d05f9918
### Tjänster exponerar kontoautentiseringsuppgifter
<a id="services-exposing-account-credentials" class="xliff"></a>
May  3 13:34:23 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|LdapSimpleBindCleartextPasswordSuspiciousActivity|Services exposing account credentials|3|start=2017-05-03T13:28:36.5159194Z app=Ldap shost=daf::220 msg=Services running on daf::220 (daf::220) expose account credentials in clear text using LDAP simple bind. cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/5909dc5f8ca1ec04d05fa8b1
### Pass the Ticket
<a id="pass-the-ticket" class="xliff"></a>
May  4 13:15:41 CENTER ATA:CEF:0|Microsoft|ATA|1.8.5942.64854|PassTheTicketSuspiciousActivity|Identity theft using Pass-the-Ticket attack|10|start=2017-05-04T13:13:44.5160000Z app=Kerberos shost=CLIENT1 suser=Administrator request=krbtgt/DOMAIN1.TEST.LOCAL msg=Administrator's Kerberos tickets were stolen from CLIENT2 to CLIENT1 and used to access krbtgt/DOMAIN1.TEST.LOCAL. cs2Label=ticketSourceComputer cs2=CLIENT2 cs3Label=ticketSourceComputerIpAddress cs3= cs1Label=url cs1=https://192.168.0.220/suspiciousActivity/590b29168ca1ec0ba438acf6

## Se även
<a id="see-also" class="xliff"></a>
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
