---
title: "Förstå Azure ATP övervakning notifieringar | Microsoft Docs"
description: "Beskriver hur du kan använda Azure ATP-loggarna för att felsöka problem"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: d0551e91-3b21-47d5-ad9d-3362df6d47c0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cdb440e92aef0f9d09d3aa9411d0ce65435469d1
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*

# <a name="understanding-azure-atp-sensor-and-standalone-sensor-monitoring-alerts"></a>Förstå Azure ATP sensor och fristående sensor övervaka aviseringar

Azure ATP Health Center får du veta när det uppstår ett problem med någon av dina Azure ATP worksapces genom att en övervakningsavisering. Den här artikeln beskriver övervakningsaviseringarna för varje komponent, samt orsaken och de steg som krävs för att åtgärda problemet.

## <a name="read-only-user-password-to-expire-shortly"></a>Skrivskyddad användarens lösenord upphör snart att

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Det skrivskyddade användarlösenordet som används för att matcha enheter mot Active Directory går ut inom 30 dagar.|Om den här användarens lösenord upphör att gälla Azure ATP sensorerna stoppas och inga nya data som samlas in.|[Ändra lösenordet för domänanslutning](modifying-atp-config-dcpassword.md) och uppdatera sedan lösenordet i Azure ATP-konsolen.|Medel|

## <a name="read-only-user-password-expired"></a>Det skrivskyddade lösenordet har upphört att gälla

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Det skrivskyddade användarlösenordet som används för att hämta katalogdata har gått ut.|Azure ATP sensorerna stoppas (eller stoppas snart) och inga nya data som samlas in.|[Ändra lösenordet för domänanslutning](modifying-atp-config-dcpassword.md) och uppdatera sedan lösenordet i Azure ATP-konsolen.|Hög|

## <a name="domain-synchronizer-not-assigned"></a>Ingen domänsynkroniserare har tilldelats

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Någon domänsynkroniserare tilldelas till någon Azure ATP sensor. Detta kan inträffa om det finns inga Azure ATP-sensor som konfigurerats som kandidat för domänsynkronisering.|När domänen inte har synkroniserats kan orsaka entitetsinformation i Azure ATP ska bli saknas eller är för gammal entitetsändringar men påverkar inte någon identifiering.|Se till att minst en Azure ATP-sensor har angetts som en [domänsynkroniserare](install-atp-step5.md).|Låg|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>Alla/vissa avbilda nätverkskort på en sensor är inte tillgängliga

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Alla/vissa av de valda avbilda nätverkskorten på Azure ATP-temperatursensor är inaktiverad eller frånkopplad.|Nätverkstrafik för vissa/alla domänkontrollanter fångas inte längre av Azure ATP sensorn. Detta påverkar möjligheten att identifiera misstänkta aktiviteter som rör dessa domänkontrollanter.|Kontrollera att dessa valda avbilda nätverkskort på Azure ATP-sensor är aktiverat och anslutet.|Medel|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>Vissa domänkontrollanter inte kan nås av en sensor

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|En Azure ATP sensor har begränsad funktionalitet på grund av problem med nätverksanslutningen till vissa av de konfigurerade domänkontrollanterna.|Skicka Hash-identifiering kan vara mindre exakt när vissa domänkontrollanter kan inte frågas av Azure ATP sensorn.|Kontrollera att domänkontrollanterna är igång och att den här Azure ATP sensor kan öppna LDAP-anslutningar till dem.|Medel|

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>Alla domänkontrollanter inte kan nås av en sensor

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Azure ATP-sensor är offline på grund av problem med nätverksanslutningen till de konfigurerade domänkontrollanterna.|Detta påverkar Azure ATP möjlighet att identifiera misstänkta aktiviteter relaterade till domänkontrollanter som övervakas av den här Azure ATP sensorn.| Kontrollera att domänkontrollanterna är igång och att den här Azure ATP sensor kan öppna LDAP-anslutningar till dem.|Medel|

## <a name="sensor-stopped-communicating"></a>temperatursensor stoppats kommunikation

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Ingen kommunikation från Azure ATP sensorn har uppstått. Standardtidsintervallet för den här aviseringen är fem minuter.|Nätverkskortet på Azure ATP-sensor avbildas inte längre nätverkstrafik. Detta påverkar ATA: s möjlighet att identifiera misstänkta aktiviteter eftersom nätverkstrafik inte kommer att nå Azure ATP-Molntjänsten.|Kontrollera att den port som används för kommunikation mellan Azure ATP sensor och Azure ATP-Molntjänsten inte blockeras av alla routrar och brandväggar.|Medel|

## <a name="no-traffic-received-from-domain-controller"></a>Ingen trafik togs emot från domänkontrollanten

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Ingen trafik togs emot från domänkontrollanten via den här Azure ATP sensorn.|Detta kan tyda på att portspegling från domänkontrollanterna till Azure ATP-sensor ännu inte har konfigurerats eller fungerar inte.|Kontrollera att [portspegling är korrekt konfigurerat på dina nätverksenheter](configure-port-mirroring.md).<br></br>Avbilda nätverkskort på Azure ATP-sensor kan inaktivera dessa funktioner i avancerade inställningar:<br></br>Sammanslagning av mottagna segment, RSC (IPv4)<br></br>Sammanslagning av mottagna segment, RSC (IPv6)|Medel|

## <a name="some-forwarded-events-are-not-being-analyzed"></a>Vissa vidarebefordrade händelser analyseras inte

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Azure ATP-sensor emot fler händelser än kan bearbetas.|Vissa vidarebefordrade händelser analyseras inte, vilket kan påverka möjligheten att identifiera misstänkta aktiviteter från domänkontrollanter som övervakas av den här Azure ATP sensorn.|Kontrollera att endast nödvändiga händelser vidarebefordras till Azure ATP-sensor eller försöker vidarebefordra vissa av händelserna till en annan Azure ATP sensor.|Medel|

## <a name="some-network-traffic-is-not-being-analyzed"></a>En del nätverkstrafik analyseras inte

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Azure ATP-sensor tar emot mer trafik än vad som kan bearbetas.|Nätverkstrafik analyseras inte, vilket kan påverka möjligheten att identifiera misstänkta aktiviteter från domänkontrollanter som övervakas av den här Azure ATP sensorn.|Överväg att [lägga till fler processorer och mer minne](atp-capacity-planning.md) om det behövs. Om detta är en fristående Azure ATP sensor kan minska antalet domänkontrollanter som övervakas.<br></br>Detta kan också inträffa om du använder domänkontrollanter på virtuella VMware-datorer. För att undvika dessa aviseringar kan du kontrollera att följande inställningar är inställda på 0 eller inaktiverade i den virtuella datorn:<br></br>-TsoEnable<br></br>- LargeSendOffload(IPv4)<br></br>-IPv4 Systemansvarig avlastning<br></br>Du kan även inaktivera IPv4 Giant TSO Offload. Mer information finns i dokumentationen för VMware.|Medel|

## <a name="sensor-service-failed-to-start"></a>sensor-tjänsten kunde inte startas

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Azure ATP sensor-tjänsten kunde inte starta minst 30 minuter.|Detta kan påverka möjligheten att identifiera misstänkta aktiviteter från domänkontrollanter som övervakas av den här Azure ATP sensorn.|Övervaka Azure ATP sensor loggar för att förstå orsaken till Azure ATP sensor tjänstfel.|Hög|

## <a name="sensor-reached-a-memory-resource-limit"></a>temperatursensor nått en minnesgräns för resurs

|Varning|Description|Lösning|Allvarlighetsgrad|
|----|----|----|----|
|Azure ATP-sensor stoppas sig själv och startas om automatiskt för att skydda domänkontrollanten från lite minne.|Azure ATP-sensor framtvingar begränsningar i minnet på sig själv för att förhindra att domänkontrollanten upplever resursbegränsningar. Detta händer när minnesanvändningen på domänkontrollanten är hög. Data från den här domänkontrollanten övervakas endast delvis.|Öka mängden minne (RAM) på domänkontrollanten eller lägg till fler domänkontrollanter på den här platsen så att domänkontrollantens belastning fördelas bättre.|Medel|


## <a name="see-also"></a>Se även

- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)