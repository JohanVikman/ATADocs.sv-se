---
title: Förstå Azure ATP-övervakningsaviseringar | Microsoft Docs
description: Beskriver hur du kan använda Azure ATP-loggarna för att felsöka problem
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/15/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: d0551e91-3b21-47d5-ad9d-3362df6d47c0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7cffaef77a80b5c1c9bb33694ef2c7a73ef80ee0
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166926"
---
*Gäller för: Azure Avancerat skydd*

# <a name="understanding-azure-atp-sensor-and-standalone-sensor-monitoring-alerts"></a>Förstå Azure ATP-sensorn och fristående sensorn övervakningsaviseringar

Azure ATP Health Center får du veta när det uppstår ett problem med någon av dina Azure ATP-arbetsytor genom att en övervakningsavisering. Den här artikeln beskriver övervakningsaviseringarna för varje komponent, samt orsaken och de steg som krävs för att åtgärda problemet.

## <a name="read-only-user-password-to-expire-shortly"></a>Skrivskyddade användarlösenordet upphör snart att gälla

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Det skrivskyddade användarlösenordet som används för att matcha enheter mot Active Directory går ut inom 30 dagar.|Om den här användarens lösenord upphör att gälla, stoppas alla Azure ATP-sensorer och inga nya data som samlas in.|[Ändra lösenord för domänanslutning](modifying-atp-config-dcpassword.md) och uppdatera sedan lösenordet i Azure ATP-konsolen.|Medel|

## <a name="read-only-user-password-expired"></a>Det skrivskyddade lösenordet har upphört att gälla

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Det skrivskyddade användarlösenordet som används för att hämta katalogdata har gått ut.|Alla Azure ATP-sensorer stoppas (eller slutar snart) och inga nya data som samlas in.|[Ändra lösenord för domänanslutning](modifying-atp-config-dcpassword.md) och uppdatera sedan lösenordet i Azure ATP-konsolen.|Hög|

## <a name="domain-synchronizer-not-assigned"></a>Ingen domänsynkroniserare har tilldelats

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Ingen domänsynkroniserare har tilldelats någon Azure ATP-sensorn. Detta kan inträffa om det finns inga Azure ATP-sensorn som konfigurerats som kandidat för domänsynkronisering.|När domänen inte synkroniseras ändringarna till entiteter kan göra att entitetsinformation i Azure ATP blir inaktuell eller saknas, men påverkar inte någon identifiering.|Se till att minst en Azure ATP-sensorn har angetts som en [domänsynkroniserare](install-atp-step5.md).|Låg|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>Alla/vissa av nätverkskorten för inhämtning på en sensor är inte tillgängliga

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Alla/vissa av de valda insamlingsnätverkskort på Azure ATP-sensorn är inaktiverade eller bortkopplade.|Nätverkstrafik för vissa/alla domänkontrollanter samlas inte längre av Azure ATP-sensorn. Detta påverkar möjligheten att identifiera misstänkta aktiviteter relaterade till dessa domänkontrollanter.|Kontrollera att dessa valda insamlingsnätverkskort på Azure ATP-sensorn är aktiverade och anslutna.|Medel|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>Vissa domänkontrollanter kan nås av en sensor

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Azure ATP-sensorn har begränsad funktionalitet på grund av anslutningsproblem till några av de konfigurerade domänkontrollanterna.|Pass Hash-identifiering kan vara mindre exakta när vissa domänkontrollanter kan inte frågas genom Azure ATP-sensorn.|Kontrollera att domänkontrollanterna är igång och körs och att den här Azure ATP-sensorn kan öppna LDAP-anslutningar till dem.|Medel|

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>Alla domänkontrollanter kan nås av en sensor

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Azure ATP-sensorn är för närvarande frånkopplad på grund av anslutningsproblem till alla konfigurerade domänkontrollanter.|Detta påverkar Azure ATP-förmåga att identifiera misstänkta aktiviteter relaterade till domänkontrollanter som övervakas av den här Azure ATP-sensorn.| Kontrollera att domänkontrollanterna är igång och körs och att den här Azure ATP-sensorn kan öppna LDAP-anslutningar till dem.|Medel|

## <a name="sensor-stopped-communicating"></a>Sensorn slutade kommunicera

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Det har skett någon kommunikation från Azure ATP-sensorn. Standardtidsintervallet för den här aviseringen är fem minuter.|Nätverkstrafik samlas inte längre av nätverkskort på Azure ATP-sensorn. Detta påverkar ATA: s möjlighet att identifiera misstänkta aktiviteter eftersom nätverkstrafiken inte kan nå Azure ATP-Molntjänsten.|Kontrollera att den port som används för kommunikation mellan Azure ATP-sensorn och Azure ATP-Molntjänsten inte blockeras av några routrar eller brandväggar.|Medel|

## <a name="no-traffic-received-from-domain-controller"></a>Ingen trafik togs emot från domänkontrollanten

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Ingen trafik togs emot från domänkontrollanten via den här Azure ATP-sensorn.|Detta kan tyda på att portspegling från domänkontrollanterna till Azure ATP-sensorn ännu inte har konfigurerats eller fungerar inte.|Kontrollera att [portspegling är korrekt konfigurerat på dina nätverksenheter](configure-port-mirroring.md).<br></br>På Azure ATP-sensorn nätverkskort för datainsamling, inaktivera dessa funktioner i avancerade inställningar:<br></br>Sammanslagning av mottagna segment, RSC (IPv4)<br></br>Sammanslagning av mottagna segment, RSC (IPv6)|Medel|

## <a name="some-forwarded-events-are-not-being-analyzed"></a>Vissa vidarebefordrade händelser analyseras inte

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Azure ATP-sensorn tar emot fler händelser än den kan bearbeta.|Vissa vidarebefordrade händelser analyseras inte, vilket kan påverka möjligheten att identifiera misstänkta aktiviteter från domänkontrollanter som övervakas av den här Azure ATP-sensorn.|Kontrollera att endast nödvändiga händelser vidarebefordras till Azure ATP-sensorn eller prova att vidarebefordra vissa händelser till en annan Azure ATP-sensorn.|Medel|

## <a name="some-network-traffic-is-not-being-analyzed"></a>En del nätverkstrafik analyseras inte

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Azure ATP-sensorn tar emot mer nätverkstrafik än den kan bearbeta.|En del nätverkstrafik analyseras inte, vilket kan påverka möjligheten att identifiera misstänkta aktiviteter från domänkontrollanter som övervakas av den här Azure ATP-sensorn.|Överväg att [lägga till fler processorer och mer minne](atp-capacity-planning.md) om det behövs. Om det här är ett fristående Azure ATP-sensorn, minska antalet domänkontrollanter som övervakas.<br></br>Detta kan också inträffa om du använder domänkontrollanter på virtuella VMware-datorer. För att undvika dessa aviseringar kan du kontrollera att följande inställningar är inställda på 0 eller inaktiverade i den virtuella datorn:<br></br>-TsoEnable<br></br>-LargeSendOffload(IPv4)<br></br>-IPv4 TSO avlastning<br></br>Du kan även inaktivera IPv4 Giant TSO Offload. Mer information finns i dokumentationen om VMware.|Medel|

## <a name="sensor-service-failed-to-start"></a>Det gick inte att starta sensortjänsten

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Tjänsten Azure ATP-sensorn kunde inte starta under minst 30 minuter.|Detta kan påverka möjligheten att identifiera misstänkta aktiviteter från domänkontrollanter som övervakas av den här Azure ATP-sensorn.|Övervaka Azure ATP-sensorn loggar för att förstå den grundläggande orsaken till att Azure ATP sensortjänsten misslyckas.|Hög|

## <a name="sensor-reached-a-memory-resource-limit"></a>Sensorn uppnådde en minnesresursgräns

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Azure ATP-sensorn stoppas själva och startas om automatiskt för att skydda domänkontrollanten mot med minne.|Azure ATP-sensorn tillämpar minnesbegränsningar att förhindra att domänkontrollanten upplever resursbegränsningar. Detta händer när minnesanvändningen på domänkontrollanten är hög. Data från den här domänkontrollanten övervakas endast delvis.|Öka mängden minne (RAM) på domänkontrollanten eller lägg till fler domänkontrollanter på den här platsen så att domänkontrollantens belastning fördelas bättre.|Medel|

## <a name="sensor-outdated"></a>sensorn är inaktuell

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Azure ATP-sensorn är inaktuell.|Azure ATP-sensorn kör en version som är minst tre versioner som är inaktuell.|Uppdatera manuellt sensorn och kontroll för att se varför sensorn automatiskt uppdateras inte. Om detta inte fungerar kan du ladda ned det senaste installationspaketet för sensorn och avinstallera och installera sensorn. Mer information finns i [installerar Azure ATP-sensorn](install-atp-step4.md).|Medel|

## <a name="see-also"></a>Se även

- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)