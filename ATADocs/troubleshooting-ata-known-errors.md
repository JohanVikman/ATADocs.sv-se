---
title: "Felsöka kända problem i ATA | Microsoft Docs"
description: "Beskriver hur du kan felsöka kända problem i Advanced Threat Analytics"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/3/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 0ded0dd064f0327f6e52f15081e2b9dce14f982b
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/03/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="troubleshooting-ata-known-issues"></a>Felsöka kända problem i ATA

Det här avsnittet beskriver möjliga fel i distributionen av ATA och de steg som krävs för att felsöka dem.

## <a name="ata-gateway-and-lightweight-gateway-errors"></a>Fel i ATA Gateway och ATA Lightweight Gateway

|Fel|Beskrivning|Lösning|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException: Ett lokalt fel uppstod|ATA Gateway kunde inte autentiseras mot domänkontrollanten.|1. Bekräfta att domänkontrollantens DNS-post har konfigurerats korrekt i DNS-servern. <br>2. Kontrollera att tiden för ATA Gateway har synkroniserats med tiden för domänkontrollanten.|
|System.IdentityModel.Tokens.SecurityTokenValidationException: Kunde inte verifiera certifikatkedja|ATA Gateway kunde inte verifiera certifikatet för ATA Center.|1. Kontrollera att certifikatet från rotcertifikatutfärdaren har installerats i certifikatarkivet för betrodd certifikatutfärdare på ATA Gateway. <br>2. Verifiera att listan över återkallade certifikat (CRL) är tillgänglig och att det går att utföra verifiering av certifikatåterkallning.|
|Microsoft.Common.ExtendedException: Det gick inte att tolka skapad tid|ATA Gateway kunde inte tolka syslog-meddelanden som vidarebefordrades från SIEM.|Kontrollera att SIEM har konfigurerats för att vidarebefordra meddelandena i något av de format som stöds av ATA.|
|System.ServiceModel.FaultException: Ett fel uppstod vid verifiering av säkerheten för meddelandet.|ATA Gateway kunde inte autentiseras mot ATA Center.|Kontrollera att tiden för ATA Gateway har synkroniserats med tiden för ATA Center.|
|System.ServiceModel.EndpointNotFoundException: Det gick inte att ansluta till net.tcp://center.ip.addr:443/IEntityReceiver|ATA Gateway kunde inte upprätta en anslutning till ATA Center.|Kontrollera att nätverksinställningarna är korrekta och att nätverksanslutningen mellan ATA Gateway och ATA Center är aktiv.|
|System.DirectoryServices.Protocols.LdapException: LDAP-servern är inte tillgänglig.|ATA Gateway kunde inte skicka en fråga till domänkontrollanten med LDAP-protokollet.|1. Kontrollera att användarkontot som används av ATA för att ansluta till Active Directory-domänen har läsbehörighet för alla objekt i Active Directory-trädet. <br>2. Kontrollera att domänkontrollanten inte är i strikt läge för att förhindra LDAP-frågor från det användarkonto som används av ATA.|
|Microsoft.Tri.Infrastructure.ContractException: Kontraktundantag|ATA Gateway kunde inte synkronisera konfigurationen från ATA Center.|Slutför konfigurationen av ATA Gateway i ATA-konsolen.|
|System.Reflection.ReflectionTypeLoadException: Det gick inte att läsa in en eller flera av de begärda typerna. Hämta egenskapen LoaderExceptions för mer information.|Message Analyzer har installerats på ATA Gateway.| Avinstallera Message Analyzer.|
|Error [Layout] System.OutOfMemoryException: Undantag av typen ”System.OutOfMemoryException” uppstod.|ATA Gateway har inte tillräckligt med minne.|Öka mängden minne på domänkontrollanten.|
|Kunde inte starta livekonsumenten  ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: PEFNDIS-händelseprovidern är inte redo|PEF (Message Analyzer) har inte installerats korrekt.|Om du använder Hyper-V kan du försöka uppgradera Hyper-V-integreringstjänsterna. Kontakta annars supporten för hjälp.|
|Installationen misslyckades med felet: 0x80070652|Det finns andra väntande installationer på datorn.|Vänta tills de andra installationerna har slutförts och starta om datorn vid behov.|
|System.InvalidOperationException: Instansen Microsoft.Tri.Gateway finns inte i den angivna kategorin.|PID:er har aktiverats för processnamn i ATA-gatewayen|Använd [KB281884](https://support.microsoft.com/en-us/kb/281884) för att inaktivera PID:er i processnamn|
|System.InvalidOperationException: Kategorin finns inte.|Räknare kan vara inaktiverade i registret|Använd [KB2554336](https://support.microsoft.com/en-us/kb/2554336) för att återskapa prestandaräknare|
|System.ApplicationException: Det går inte att starta ETW-session MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329|Det finns en värdpost i HOSTS-filen som pekar på datorns kortnamn|Ta bort posten värden från C:\Windows\System32\drivers\etc\HOSTS-fil eller ändra den till ett fullständigt domännamn.|
|System.IO.IOException: Autentiseringen misslyckades eftersom den fjärranslutna parten har stängt transportströmmen.|TLS 1.0 är inaktiverat på ATA-gatewayen men .Net är inställd att använda TLS 1.2|Använd ett av följande alternativ: </br> Aktivera TLS 1.0 på ATA-gatewayen </br>Aktivera TLS 1.2 på .Net genom att ställa in registernycklarna att använda operativsystemets standarder för LLS och TLS enligt följande: `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`|
|System.TypeLoadException: Det gick inte att läsa in typen 'Microsoft.Opn.Runtime.Values.BinaryValueBufferManager' från sammansättningen 'Microsoft.Opn.Runtime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'|ATA Gateway kunde inte läsa in de nödvändiga parsningsfilerna.|Kontrollera om Analysverktyg för meddelanden är installerat. Analysverktyg för meddelanden kan inte installeras med ATA Gateway/ATA Lightweight Gateway. Avinstallera Analysverktyg för meddelanden och starta om gatewaytjänsten.|
|Aviseringar om ignorerad portspeglingstrafik när Lightweight Gateway används på VMware|Om du använder domänkontrollanter på virtuella VMware-datorer kan du få aviseringar om **ignorerad portspeglingstrafik**. Detta kan inträffa på grund av ett konfigurationsmatchningsfel i VMware. |För att undvika dessa aviseringar kan du kontrollera att följande inställningar är inställda på 0 eller inaktiverade: TsoEnable, LargeSendOffload, IPv4, TSO Offload. Du kan även inaktivera IPv4 Giant TSO Offload. Mer information finns i dokumentationen om VMware.|


## <a name="deployment-errors"></a>Distributionsfel
|Fel|Beskrivning|Lösning|
|-------------|----------|---------|
|Installationen av .Net Framework 4.6.1 misslyckas med fel 0x800713ec|Kraven för .Net Framework 4.6.1 är inte installerade på servern. |Kontrollera att Windows-uppdateringarna [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) och [KB2919355](https://support.microsoft.com/kb/2919355) är installerade på servern innan ATA installeras.|
|System.Threading.Tasks.TaskCanceledException: En uppgift avbröts|Tidsgränsen för distributionsprocessen gick ut eftersom det inte gick att nå ATA Center.|1.    Kontrollera nätverksanslutningen till ATA Center genom att ansluta till tjänsten med hjälp av dess IP-adress. <br></br>2.    Kontrollera proxy- eller brandväggskonfigurationerna.|
|System.Net.Http.HttpRequestException: Ett fel uppstod när begäran skickades. ---> System.Net.WebException: Fjärrservern returnerade ett fel: 407 - Proxy-autentisering krävs.|Tidsgränsen för distributionsprocessen gick ut eftersom det inte gick att nå ATA Center på grund av en felaktig proxykonfiguration.|Inaktivera proxykonfigurationen före distributionen och aktivera sedan proxykonfigurationen igen. Du kan också konfigurera ett undantag i proxyn.|
|Ingen trafik togs emot från domänkontrollanten, men övervakningsaviseringar observeras|    Ingen trafik togs emot från en domänkontrollant med hjälp av portspegling via en ATA-gateway|Inaktivera följande funktioner i **Avancerade inställningar** på ATA-gatewayens nätverkskort för datainsamling:<br></br>Sammanslagning av mottagna segment, RSC (IPv4)<br></br>Sammanslagning av mottagna segment, RSC (IPv6)|





## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)