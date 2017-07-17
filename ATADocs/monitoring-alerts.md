---
title: "Förstå ATA-övervakningsaviseringar | Microsoft Docs"
description: "Beskriver hur du kan använda ATA-loggarna för att felsöka problem"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/13/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: b04fb8a4-b366-4b55-9d4c-6f054fa58a90
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4c232ea6bd25f1f13fe8e322719cda6388da9c0e
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/30/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



ATA Health Center genererar en övervakningsavisering om det uppstår problem med ATA-distributionen.
Den här artikeln beskriver övervakningsaviseringarna för varje komponent, samt orsaken och de steg som krävs för att åtgärda problemet.
## Problem med ATA Center
<a id="ata-center-issues" class="xliff"></a>
### ATA Center börjar få ont om diskutrymme
<a id="ata-center-running-out-of-disk-space" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Det lediga utrymmet på ATA Center-disken som används för att lagra ATA-databasen börjar ta slut.|Det betyder att hårddisken har mindre än 200 GB ledigt utrymme eller att det finns mindre än 20 % ledigt utrymme kvar, beroende på vilket som är minst. När ATA märker att enheten börjar få slut på lagringsutrymme börjar tjänsten ta bort gamla data från databasen. Den här aviseringen genereras om det inte går att ta bort gamla data eftersom tjänsten fortfarande behöver dem för identifieringsmotorn. Om du får den här aviseringen betyder det att ATA har slutat att spåra nya aktiviteter.|Öka diskens storlek eller frigör utrymme på disken.|Hög|
### Det går inte att skicka e-post
<a id="failure-sending-mails" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|ATA kunde inte skicka en e-postavisering till den angivna e-postservern.|Inga e-postmeddelanden skickas från ATA.|Kontrollera SMTP-serverkonfigurationen.|Låg|

### ATA Center är överbelastat
<a id="ata-center-overloaded" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|ATA Center kan inte hantera mängden data som överförs från ATA-gatewayerna. |ATA Center slutar att analysera ny nätverkstrafik och nya händelser. Det innebär att identifieringarnas och profilernas exakthet minskar när den här övervakningsaviseringen är aktiv.|Kontrollera att ATA Center har tilldelats tillräckligt med resurser. Mer information om hur du planerar kapaciteten för ATA Center finns i avsnittet om [kapacitetsplanering för ATA](ata-capacity-planning.md). Undersök ATA Centers prestanda med hjälp av informationen i avsnittet [Felsöka ATA med prestandaräknarna](troubleshooting-ata-using-perf-counters.md).|Hög|

### Det går inte att ansluta till SIEM-servern med hjälp av Syslog
<a id="failure-connecting-to-the-siem-server-using-syslog" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|ATA kunde inte skicka händelser till den angivna SIEM-servern.|Det innebär att ATA Center inte kan skicka misstänkta aktiviteter och övervakningsaviseringar till din SIEM-server.|Kontrollera att [Syslog-serverinställningarna är rätt konfigurerade](setting-syslog-email-server-settings.md).|Låg|
### ATA Center-certifikatet upphör snart att gälla
<a id="ata-center-certificate-is-about-to-expire" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|ATA Center-certifikatet går ut inom tre veckor.|När certifikatet har gått ut misslyckas anslutningar från ATA-gatewayer till ATA Center. ATA Center-processen kraschar och alla ATA-funktioner stoppas.|[Ersätt ATA Center-certifikatet](modifying-ata-center-configuration.md)|Medel|
### ATA Center-certifikatet har upphört att gälla
<a id="ata-center-certificate-expired" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|ATA Center-certifikatet har gått ut.|När certifikatet har gått ut misslyckas anslutningar från ATA-gatewayerna till ATA Center. ATA Center-processen kraschar och alla ATA-funktioner stoppas.|[Ersätt ATA Center-certifikatet](modifying-ata-center-configuration.md)|Hög|
## Problem med ATA Gateway
<a id="ata-gateway-issues" class="xliff"></a>
### Det skrivskyddade användarlösenordet upphör snart att gälla
<a id="read-only-user-password-is-about-to-expire" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Det skrivskyddade användarlösenordet som används för att matcha enheter mot Active Directory går ut inom 30 dagar.|Om lösenordet för den här användaren går ut slutar alla ATA-gatewayer att köra och inga nya data samlas in.|[Ändra lösenordet för domänanslutningar](modifying-ata-config-dcpassword.md) och uppdatera sedan lösenordet i ATA-konsolen.|Medel|
### Det skrivskyddade lösenordet har upphört att gälla
<a id="read-only-user-password-expired" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Det skrivskyddade användarlösenordet som används för att hämta katalogdata har gått ut.|Alla ATA-gatewayer slutar att köra (eller gör det snart) och inga nya data samlas in.|[Ändra lösenordet för domänanslutningar](modifying-ata-config-dcpassword.md) och uppdatera sedan lösenordet i ATA-konsolen.|Hög|
### ATA Gateway-certifikatet upphör snart att gälla
<a id="ata-gateway-certificate-about-to-expire" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|ATA Gateway-certifikatet går ut inom tre veckor.|Anslutningar från den specifika ATA-gatewayen till ATA Center misslyckas. Inga data från den aktuella ATA-gatewayen skickas.|ATA Gateway-certifikatet borde ha förnyats automatiskt. Granska loggarna för ATA Gateway och ATA Center för att ta reda på varför certifikatet inte förnyades automatiskt.|Medel|

### ATA Gateway-certifikatet har upphört att gälla
<a id="ata-gateway-certificate-expired" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|ATA Gateway-certifikatet har gått ut.|Det finns ingen anslutning från den här ATA-gatewayen till ATA Center. Inga data från den aktuella ATA-gatewayen skickas.|[Avinstallera och installera om ATA Gateway](install-ata-step3.md).|Hög|
### Ingen domänsynkroniserare har tilldelats
<a id="domain-synchronizer-not-assigned" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Inga ATA-gatewayer har tilldelats en domänsynkroniserare. Detta kan inträffa om det inte finns någon ATA-gateway som har konfigurerats som kandidat för domänsynkronisering.|När domänen inte synkroniseras kan entitetsändringar resultera i att entitetsinformation i ATA blir inaktuell eller saknas, men identifieringen påverkas inte.|Kontrollera att minst en ATA-gateway har angetts som en [domänsynkroniserare](install-ata-step5.md).|Låg|
### Alla/vissa insamlingsnätverkskort på en ATA-gateway är inte tillgängliga
<a id="allsome-of-the-capture-network-adapters-on-an-ata-gateway-are-not-available" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Alla/vissa av de valda insamlingsnätverkskorten på ATA-gatewayen är inaktiverade eller frånkopplade.|Nätverkstrafik för vissa/alla domänkontrollanter samlas inte längre in av ATA-gatewayen. Detta påverkar möjligheten att identifiera misstänkta aktiviteter relaterade till dessa domänkontrollanter.|Kontrollera att dessa valda insamlingsnätverkskort på ATA-gatewayen är aktiverade och anslutna.|Medel|
### Vissa domänkontrollanter kan inte nås av en ATA-gateway
<a id="some-domain-controllers-are-unreachable-by-a-ata-gateway" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|En ATA-gateway har begränsad funktionalitet på grund av anslutningsproblem med vissa av de konfigurerade domänkontrollanterna.|”Pass the Hash”-identifieringar kan vara mindre exakta när ATA-gatewayen inte kan hämta data från vissa domänkontrollanter.|Kontrollera att domänkontrollanterna körs och att ATA-gatewayen kan öppna LDAP-anslutningar till dem.|Medel|
### Inga domänkontrollanter kan nås av en ATA-gateway
<a id="all-domain-controllers-are-unreachable-by-a-ata-gateway" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|ATA-gatewayen är för närvarande frånkopplad på grund av anslutningsproblem med alla konfigurerade domänkontrollanter.|Detta påverkar ATA:s möjlighet att identifiera misstänkta aktiviteter relaterade till domänkontrollanter som övervakas av den här ATA-gatewayen.| Kontrollera att domänkontrollanterna körs och att ATA-gatewayen kan öppna LDAP-anslutningar till dem.|Medel|
### ATA-gatewayen slutade kommunicera
<a id="ata-gateway-stopped-communicating" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Det har inte skett någon kommunikation från ATA-gatewayen. Standardtidsintervallet för den här aviseringen är fem minuter.|Nätverkstrafik samlas inte längre in av nätverkskortet på ATA-gatewayen. Detta påverkar ATA:s möjlighet att identifiera misstänkta aktiviteter eftersom nätverkstrafiken inte kan nå ATA Center.|Kontrollera att porten som används för kommunikation mellan ATA Gateway- och ATA Center-tjänsten inte blockeras av några routrar eller brandväggar.|Medel|
### Ingen trafik togs emot från domänkontrollanten
<a id="no-traffic-received-from-domain-controller" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Ingen trafik togs emot från domänkontrollanten via den här ATA-gatewayen.|Detta kan bero på att portspegling från domänkontrollanterna till ATA Gateway inte fungerar eller inte har konfigurerats än.|Kontrollera att [portspegling är korrekt konfigurerat på dina nätverksenheter](configure-port-mirroring.md).|Medel|
### Vissa vidarebefordrade händelser analyseras inte
<a id="some-forwarded-events-are-not-being-analyzed" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|ATA-gatewayen tar emot fler händelser än den kan bearbeta.|Vissa vidarebefordrade händelser analyseras inte, vilket kan påverka möjligheten att identifiera misstänkta aktiviteter från domänkontrollanter som övervakas av ATA-gatewayen.|Kontrollera att endast nödvändiga händelser vidarebefordras till ATA-gatewayen eller prova att vidarebefordra vissa av händelserna till en annan ATA-gateway.|Medel|
### En del nätverkstrafik analyseras inte
<a id="some-network-traffic-is-not-being-analyzed" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|ATA-gatewayen tar emot mer trafik än den kan bearbeta.|En del nätverkstrafik analyseras inte, vilket kan påverka möjligheten att identifiera misstänkta aktiviteter från domänkontrollanter som övervakas av ATA-gatewayen.|Överväg att [lägga till fler processorer och mer minne](ata-capacity-planning.md) om det behövs. Om detta är en fristående ATA-gateway kan du minska antalet domänkontrollanter som övervakas.|Medel|

### ATA Gateway-versionen är inaktuell
<a id="ata-gateway-version-outdated" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|ATA Center är nyare än den version som är installerad på ATA-gatewayen. Detta gör att ATA Gateway-tjänsten inte fungerar som förväntat.|Detta kan påverka möjligheten att identifiera misstänkta aktiviteter från domänkontrollanter som övervakas av ATA-gatewayen.|Uppdatera ATA Gateway till den senaste versionen automatiskt genom att aktivera funktionen för [automatiska uppdateringar](install-ata-step1.md) i ATA-konsolen eller genom att ladda ned det senaste ATA Gateway-paketet i ATA-konsolen.|Hög|
### ATA Gateway-tjänsten kunde inte starta
<a id="ata-gateway-service-failed-to-start" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|ATA Gateway-tjänsten kunde inte starta under minst 30 minuter.|Detta kan påverka möjligheten att identifiera misstänkta aktiviteter från domänkontrollanter som övervakas av ATA-gatewayen.|Granska ATA Gateway-loggarna för att [ta reda på rotorsaken till att ATA Gateway-tjänsten misslyckades](troubleshooting-ata-using-logs.md).|Hög|
## Lightweight Gateway
<a id="lightweight-gateway" class="xliff"></a>
### Lightweight ATA Gateway har nått en gräns för minnesresurser
<a id="lightweight-ata-gateway-reached-a-memory-resource-limit" class="xliff"></a>
|Varning|Beskrivning|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|ATA Lightweight Gateway stoppades och startar om automatiskt för att skydda domänkontrollanten mot en situation med för lite minne.|ATA Lightweight Gateway tillämpar minnesbegränsningar för att förhindra att domänkontrollanten får problem på grund av resursbegränsningar. Detta händer när minnesanvändningen på domänkontrollanten är hög. Data från den här domänkontrollanten övervakas endast delvis.|Öka mängden minne (RAM) på domänkontrollanten eller lägg till fler domänkontrollanter på den här platsen så att domänkontrollantens belastning fördelas bättre.|Medel|


## Se även
<a id="see-also" class="xliff"></a>
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
