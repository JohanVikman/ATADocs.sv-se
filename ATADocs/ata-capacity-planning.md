---
title: Planera din Advanced Threat Analytics-distribution | Microsoft Docs
description: Hjälper dig att planera distributionen och bestämma hur många ATA-servrar som krävs för nätverket
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.service: advanced-threat-analytics
ms.prod: ''
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 0b136a04f2a79e3bf8870cbbf6a4f953010cfd78
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44125846"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="ata-capacity-planning"></a>ATA-kapacitetsplanering
Den här artikeln hjälper dig att avgöra hur många ATA-servrar behövs för att övervaka ditt nätverk. Det hjälper dig att ta reda på hur många ATA-gatewayer och/eller ATA Lightweight-gatewayer du behöver samt serverkapaciteten för ATA Center och ATA-gatewayer.

> [!NOTE] 
> ATA Center kan distribueras hos valfri IaaS-leverantör så länge prestandakraven som beskrivs i den här artikeln uppfylls.

## <a name="using-the-sizing-tool"></a>Använda storleksverktyget
Det rekommenderade och enklaste sättet att avgöra kapaciteten för ATA-distributionen är genom att använda [ATA-storleksverktyget](http://aka.ms/atasizingtool). Kör ATA-storleksverktyget och använd följande fält från resultaten i Excel-filen för att avgöra vilken ATA-kapacitet du behöver:

- ATA Center – Processor och minne: Matcha fältet **Upptagna paket/sek** i ATA-Center-tabellresultatfilen med fältet **PAKET PER SEKUND** i [ATA Center-tabellen](#ata-center-sizing).

- ATA Center – Lagring: Matcha fältet **Gmsn paket/sek** i ATA Center-tabellresultatfilen med fältet **PAKET PER SEKUND** i [ATA Center-tabellen](#ata-center-sizing).
- ATA Gateway: Matcha fältet **Upptagna paket/sek** i tabellen ATA Gateway i resultatfilen med fältet **PAKET PER SEKUND** i [tabellen ATA Gateway](#ata-gateway-sizing) eller [tabellen ATA Lightweight Gateway](#ata-lightweight-gateway-sizing), beroende på vilken [gatewaytyp du väljer](#choosing-the-right-gateway-type-for-your-deployment).


![Exempel på kapacitetsplaneringsverktyg](media/capacity tool.png)


> [!NOTE]
> Eftersom olika miljöer kan variera och har flera trafikmönster för särskilda och oväntat nätverk, när du först distribuera ATA och kör storleksverktyget, kan du behöva justera och finjustera din distribution för kapacitet.


Om du av någon anledning inte kan använda ATA-storleksverktyget samlar du manuellt in informationen om paket/sek från alla dina domänkontrollanter under 24 timmar med ett lågt insamlingsintervall (ca 5 sekunder). För varje domänkontrollant måste du sedan beräkna dagligt genomsnitt och genomsnitt för den mest hektiska perioden (15 minuter).
I följande avsnitt finns anvisningar om hur du samlar in information om paket/sek från en domänkontrollant.


> [!NOTE]
> Eftersom olika miljöer kan variera och har flera trafikmönster för särskilda och oväntat nätverk, när du först distribuera ATA och kör storleksverktyget, kan du behöva justera och finjustera din distribution för kapacitet.


### <a name="ata-center-sizing"></a>Storlek för ATA Center
ATA Center kräver minst 30 dagars data enligt rekommendation för analys av användarbeteende.
 

|Paket per sekund från alla domänkontrollanter|CPU (kärnor&#42;)|Minne (GB)|Databaslagring per dag (GB)|Databaslagring per månad (GB)|IOPS&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1,000|2|32|0,3|9|30 (100)
|40,000|4|48|12|360|500 (750)
|200,000|8|64|60|1,800|1,000 (1,500)
|400 000|12|96|120|3,600|2,000 (2,500)
|750 000|24|112|225|6 750|2 500 (3 000)
|1 000 000|40|128|300|9,000|4,000 (5,000)

&#42;Detta omfattar fysiska kärnor, inte hypertrådade kärnor.

&#42;&#42;Genomsnittligt antal (högsta antal)
> [!NOTE]
> -   ATA Center kan hantera sammanlagt högst 1 miljon paket per sekund från alla övervakade domänkontrollanter. I vissa miljöer kan samma ATA Center hantera övergripande trafik som är högre än 1 miljon. Kontakta askcesec@microsoft.com för hjälp med den här typen av miljöer.
> -   Om det lediga utrymmet når minst 20% eller 200 GB, den äldsta Datasamlingen har tagits bort. Om det inte är möjligt att minska insamling av data till den här nivån har loggas en varning.  ATA ska fortsätta att fungera tills tröskelvärdet på 5% eller 50 GB ledigt har nåtts.  Nu kan ATA slutar att fylla i databasen och en ytterligare avisering kommer att utfärdas.
> - Det går att distribuera ATA Center hos valfri IaaS-leverantör så länge prestandakraven som beskrivs i den här artikeln uppfylls.
> -   Lagringssvarstiden för läs- och skrivaktiviteter bör vara under 10 ms.
> -   Förhållandet mellan läs- och skrivaktiviteter är cirka 1:3 under 100 000 paket per sekund och 1:6 över 100 000 paket per sekund.
> -   Vid körning som virtuell dator stöds inte dynamiskt minne och andra funktioner för ballongminne.
> -   För optimala prestanda ställer du in **Energialternativ** för ATA Center på **Höga prestanda**.<br>
> -   När du arbetar på en fysisk server kräver ATA-databasen att du **inaktiverar** NUMA (Non-Uniform Memory Access) i BIOS. NUMA kan kallas för Node Interleaving i ditt system. I så fall måste du **aktivera** Node Interleaving för att inaktivera NUMA. Mer information finns i BIOS-dokumentationen. Detta gäller inte om ATA Center körs på en virtuell server.


## <a name="choosing-the-right-gateway-type-for-your-deployment"></a>Välja rätt gateway-typ för distributionen
I en ATA-distribution stöds valfri kombination av ATA Gateway-typer:

- Endast ATA-gatewayer
- Endast ATA Lightweight-gatewayer
- En kombination av båda

Ha följande fördelar i åtanke när du väljer typ av Gateway-distribution:

|Gateway-typ|Fördelar|Kostnad|Distributionstopologi|Användning av domänkontrollant|
|----|----|----|----|-----|
|ATA Gateway|Out-of-band-distribution gör det svårare för angripare att upptäcka ATA|Högre|Installeras tillsammans med domänkontrollanten (out-of-band)|Har stöd för upp till 50 000 paket per sekund|
|ATA Lightweight Gateway|Kräver inte en dedikerad server och portspeglingskonfiguration|Lägre|Installerad på domänkontrollanten|Har stöd för upp till 10 000 paket per sekund|

Följande är exempel på scenarier där domänkontrollanter bör omfattas av ATA Lightweight Gateway:


- Avdelningskontor

- Virtuella domänkontrollanter som är distribuerade i molnet (IaaS)


Följande är exempel på scenarier där domänkontrollanter bör omfattas av ATA Gateway:


- Datacenter på huvudkontor (med domänkontrollanter med fler än 10 000 paket per sekund)


### <a name="ata-lightweight-gateway-sizing"></a>Storlek för ATA Lightweight Gateway

En ATA Lightweight Gateway kan stödja övervakning av en domänkontrollant baserat på mängden nätverkstrafik som domänkontrollanten genererar. 


|Paket per sekund&#42;|CPU (kärnor&#42;&#42;)|Minne (GB)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1,000|2|6|
|5 000|6|16|
    |10,000|10|24|

&#42;Totalt antal paket per sekund på domänkontrollanten som övervakas av den specifika ATA Lightweight Gateway.

&#42;&#42;Totalt antal kärnor som inte är flertrådade som är installerade på den här domänkontrollanten.<br>Även om flertrådsteknik är godkänd för ATA Lightweight Gateway bör du räkna antalet faktiska kärnor och inte flertrådade kärnor när du planerar kapaciteten.

&#42;&#42;&#42;Total mängd minne som den här domänkontrollanten har installerat.

> [!NOTE]   
> -   Domänkontrollantens prestanda påverkas inte om den inte har de resurser som krävs av ATA Lightweight Gateway, men ATA Lightweight-gatewayen kanske inte fungerar som förväntat.
> -   Vid körning som virtuell dator stöds inte dynamiskt minne och andra funktioner för ballongminne.
> -   För bästa prestanda ställer du in **Energialternativ** för ATA Lightweight Gateway på **Höga prestanda**.
> -   Minst 5 GB utrymme krävs och 10 GB rekommenderas, inklusive utrymme som krävs för ATA-binärfiler [ATA-loggarna](troubleshooting-ata-using-logs.md), och [Prestandaloggar](troubleshooting-ata-using-perf-counters.md).


### <a name="ata-gateway-sizing"></a>Storlek på ATA-gateway

Ha följande i åtanke när du avgör hur många ATA-gatewayer som ska distribueras.

-   **Active Directory-skogar och domäner**<br>
    ATA kan övervaka trafik från flera domäner från en enda Active Directory-skog. För att övervaka flera Active Directory-skogar krävs separata ATA-distributioner. Konfigurera inte en enskild ATA-distribution att övervaka nätverkstrafiken från domänkontrollanter från olika skogar.

-   **Portspegling**<br>
Överväganden för portspegling kan kräva att du distribuerar flera ATA-gatewayer per datacenter eller avdelningskontor.

-   **Kapacitet**<br>
    En ATA Gateway har stöd för övervakning av flera domänkontrollanter, beroende på mängden nätverkstrafik för de domänkontrollanter som övervakas. 
<br>



|Paket per sekund&#42;|CPU (kärnor&#42;&#42;)|Minne (GB)|
|---------------------------|-------------------------|---------------|
|1,000|1|6|
|5,000|2|10|
|10,000|3|12|
|20,000|6|24|
|50 000|16|48|

&#42;Totalt genomsnittligt antal paket per sekund från alla domänkontrollanter som övervakas av den specifika ATA-gatewayen under den tid på dagen som är mest aktiv.

&#42;Den totala mängden portspeglad trafik för domänkontrollanter får inte överskrida kapaciteten för avbildningsnätverkskortet på ATA-gatewayen.

&#42;&#42;Hypertrådning måste vara inaktiverad.

> [!NOTE] 
> -   Dynamiskt minne stöds inte.
> -   För bästa prestanda ställer du in **Energialternativ** för ATA Gateway på **Höga prestanda**.
> -   Minst 5 GB utrymme krävs och 10 GB rekommenderas, inklusive utrymme som krävs för ATA-binärfiler [ATA-loggarna](troubleshooting-ata-using-logs.md), och [Prestandaloggar](troubleshooting-ata-using-perf-counters.md).



## <a name="related-videos"></a>Relaterade videor
- [Välja rätt typ av ATA Gateway](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Se även
- [ATA-storleksverktyget](http://aka.ms/atasizingtool)
- [Krav för ATA](ata-prerequisites.md)
- [ATA-arkitektur](ata-architecture.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
