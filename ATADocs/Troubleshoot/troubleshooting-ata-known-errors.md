---
title: "Felsök felloggen i Advanced Threat Analytics | Microsoft Docs"
description: "Beskriver hur du kan felsöka vanliga fel i ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/14/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: a87fed6bf8ce69ea3391e729c57217d1cff8ffc2
ms.sourcegitcommit: a1595b51c95235eede3d3b34a02f24bedd5dfc5a
ms.translationtype: HT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/14/2017
---
*Gäller för: Advanced Threat Analytics version 1.7*



# <a name="troubleshooting-the-ata-error-log"></a>Felsöka ATA-felloggen

Det här avsnittet beskriver möjliga fel i distributionen av ATA och de steg som krävs för att felsöka dem.

## <a name="ata-gateway-errors"></a>ATA Gateway-fel

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



## <a name="ata-lightweight-gateway-errors"></a>Fel för ATA Lightweight Gateway

**Fel:** Aviseringar om ignorerad portspeglingstrafik när Lightweight Gateway används på VMware

**Beskrivning**: Om du använder domänkontrollanter på virtuella VMware-datorer kan du få aviseringar om **ignorerad portspeglingstrafik**. Detta kan inträffa på grund av ett konfigurationsmatchningsfel i VMware. 
**Lösning**: För att undvika dessa aviseringar kan du kontrollera att följande inställningar är inställda på 0 eller inaktiverade: TsoEnable, LargeSendOffload, IPv4, TSO Offload. Du kan även inaktivera IPv4 Giant TSO Offload. Mer information finns i dokumentationen om VMware.


## <a name="ata-iis-errors-not-applicable-for-ata-v17-and-above"></a>ATA IIS-fel (gäller inte för ATA v1.7 och senare)
|Fel|Beskrivning|Lösning|
|-------------|----------|---------|
|HTTP-fel 500.19 – internt serverfel|IIS URL-modulen för omarbetning installerades inte korrekt.|Avinstallera och installera om IIS-URL-modulen för omarbetning.<br>[Hämta IIS-URL-modulen för omarbetning](http://go.microsoft.com/fwlink/?LinkID=615137)|

## <a name="deployment-errors"></a>Distributionsfel
|Fel|Beskrivning|Lösning|
|-------------|----------|---------|
|Installationen av .Net Framework 4.6.1 misslyckas med fel 0x800713ec|Kraven för .Net Framework 4.6.1 är inte installerade på servern. |Kontrollera att Windows-uppdateringarna [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) och [KB2919355](https://support.microsoft.com/kb/2919355) är installerade på servern innan ATA installeras.|

![Bild för ATA .NET-installationsfel](media/netinstallerror.png)


## <a name="see-also"></a>Se även
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-kapacitetsplanering](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurera händelseinsamling](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurera vidarebefordran av Windows-händelser](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
