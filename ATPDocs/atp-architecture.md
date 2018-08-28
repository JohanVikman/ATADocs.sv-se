---
title: Azure Advanced Threat Protection-arkitektur | Microsoft Docs
description: Här beskrivs arkitekturen för Azure Advanced Threat Analytics (ATP)
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/20/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c7fda04658dc70406fc7c0d543286e46da4cfa86
ms.sourcegitcommit: 56886d06abd25035ffc9885c69aca9b0ebf14abc
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/27/2018
ms.locfileid: "43039087"
---
*Gäller för: Azure Avancerat skydd*


# <a name="azure-atp-architecture"></a>Azure ATP-arkitektur
Azure Advanced Threat Protection-arkitektur:

![Topologidiagram för Azure ATP-arkitektur](media/atp-architecture-topology.png)

Azure ATP övervakar din domänkontrollantens nätverkstrafik genom att använda portspegling till en Azure ATP fristående sensorn med fysiska eller virtuella växlar. Om du distribuerar Azure ATP-sensorn direkt på domänkontrollanterna undanröjer behovet av portspegling. Azure ATP kan också utnyttja Windows-händelser (vidarebefordras direkt från domänkontrollanterna eller från en SIEM-server) och analysera data beträffande attacker och hot. Azure ATP tar emot tolkad trafik från Azure ATP-sensorn och Azure ATP fristående sensorn. Azure ATP sedan utför profilering, kör deterministisk identifiering och kör maskininlärnings- och beteendealgoritmer för att lära sig om nätverket, aktivera identifiering av avvikelser och varna dig för misstänkta aktiviteter.

Det här avsnittet beskriver flödet i nätverk och händelseinsamling och beskriver funktionerna i huvudkomponenterna i ATP: Azure ATP-sensorn, Azure ATP fristående sensorn (som har samma grundfunktioner som Azure ATP-sensorn, men kräver ytterligare maskinvara, portspegling, konfiguration och har inte stöd för Windows ETW (Event Tracing) baserade identifieringar), och Azure ATP-Molntjänsten. 

Installerad direkt på domänkontrollanter, ATP-sensorn har åtkomst till nödvändiga händelseloggarna direkt från domänkontrollanten. När dessa loggar och nätverkstrafiken har tolkats av sensorn, skickar Azure ATP endast denna parsade information till Azure ATP-tjänsten (inte alla loggar).

## <a name="azure-atp-components"></a>Azure ATP-komponenter
Azure ATP består av följande komponenter:

-   **Azure ATP-arbetsytehanteringsportalen** <br>
Azure ATP-arbetsyteportalen för hantering kan du skapa och hantera din arbetsyta och möjliggör integrering med andra Microsoft-tjänster.

-   **Azure ATP-arbetsyteportalen** <br>
Azure ATP-arbetsyteportalen tar emot data från ATP sensorer och fristående sensorer. Den övervakar, hanterar och undersöker hoten i din miljö.

-   **Azure ATP-sensorn**<br>
Azure ATP-sensorn installeras direkt på domänkontrollanterna och övervakar trafiken direkt, utan att behöva en dedikerad server eller konfiguration av portspegling. 

-   **Azure ATP fristående sensor**<br>
Fristående Azure ATP-sensorn installeras på en dedikerad server som övervakar trafiken från domänkontrollanterna med antingen portspegling eller en nätverks-TAP. Det är ett alternativ till Azure ATP-sensorn som kräver ytterligare maskinvara, portspegling och konfiguration. Azure ATP fristående sensorer har inte stöd för Windows ETW (Event Tracing) baserade identifieringar som stöds av ATP-sensorn. 

## <a name="deployment-options"></a>Distributionsalternativ
Du kan distribuera Azure ATP med följande kombination av sensorer:

-   **Med hjälp av endast Azure ATP-sensorer**<br>
Din Azure ATP-distribution kan innehålla endast Azure ATP-sensorer: The Azure ATP-sensorer distribueras direkt på varje domänkontrollant och inga ytterligare servrar eller konfiguration av portspegling krävs.

-   **Med hjälp av endast Azure ATP fristående sensorer** <br>
Din Azure ATP-distribution kan innehålla endast Azure ATP fristående sensorer, utan någon Azure ATP-sensorer: alla domänkontrollanter måste konfigureras för att aktivera portspegling till en fristående Azure ATP-sensorn eller nätverks-TAP måste vara uppfyllda.

-   **Med både Azure ATP fristående sensorer och Azure ATP-sensorer**<br>
Din Azure ATP-distributionen omfattar både Azure ATP fristående sensorer och Azure ATP-sensorer. Azure ATP-sensorer är installerade på några av dina domänkontrollanter (till exempel alla domänkontrollanter hos avdelningskontor). På samma gång övervakas andra domänkontrollanter av Azure ATP fristående sensorer (till exempel de större domänkontrollanterna i huvuddatacentren. 


### <a name="azure-atp-management-portal"></a>Azure ATP-hanteringsportalen

Azure ATP-hanteringsportalen kan du:

-   Skapa och hantera din Azure ATP-arbetsyta

-   Integrera med andra Microsoft-säkerhetstjänster

> [!NOTE]
> - Azure ATP stöder för närvarande skapa bara en arbetsyta. När du har tagit bort en arbetsyta kan kontakta du supporten om du vill återaktivera den. Du kan ha högst tre borttagna arbetsytor. Kontakta Azure ATP-supporten om du vill öka antalet arbetsytor, och har tagits bort.
> - Om inga sensorn installeras på din arbetsyta inom 60 dagar, arbetsytan kan ha tagits bort och du måste skapa det igen.



### <a name="azure-atp-workspace-portal"></a>Azure ATP-arbetsyteportalen

Azure ATP-arbetsytan kan du hantera följande Azure ATP-funktioner:

-   Hantera Azure ATP-sensorn och fristående sensorn konfigurationsinställningar

-   Visa data som tas emot från Azure ATP fristående sensorer och Azure ATP-sensorer 

-   Övervaka identifierade misstänkta aktiviteter baserat på beteendeanalys machine learning-algoritmer för att identifiera onormalt beteende och deterministiska algoritmer för att identifiera avancerade attacker baserat på attackkedjan

-   Valfritt:, arbetsytehanteringsportalen kan konfigureras för att skicka e-post och händelser när misstänkta aktiviteter eller health-händelser som upptäcks.


|||
|-|-|
|Azure ATP-hanteringsportalen|Hanterar din Azure ATP-arbetsyta.|
|Azure ATP-arbetsyteportalen|Azure ATP-arbetsyta används för att konfigurera Azure ATP och övervaka misstänkta aktiviteter som identifieras av Azure ATP i nätverket. Azure ATP-arbetsyta är inte beroende av Azure ATP-sensorn och körs även om tjänsten Azure ATP-sensorn har stoppats. |
|Detektorer|Detektorerna använder maskininlärningsalgoritmer och deterministiska regler för att hitta misstänkta aktiviteter och onormalt användarbeteende i nätverket.|


## <a name="azure-atp-sensor-and-azure-atp-standalone-sensor"></a>Azure ATP-sensorn och Azure ATP fristående sensor

Den **Azure ATP-sensorn** och **fristående Azure ATP-sensorn** har samma grundfunktioner:

-   Samla in och inspektera nätverkstrafik på domänkontrollanter. Detta är lokal trafik på domänkontrollanten i Azure ATP-sensorer och portspeglad trafik för Azure ATP fristående sensorer. 

-   Ta emot Windows-händelser direkt från domänkontrollanterna (för ATP sensorer) eller från SIEM- eller Syslog-servrar (för ATP fristående sensorer)

-   Ta emot RADIUS-redovisningsinformation från VPN-leverantören

-   Hämta information om användare och datorer från Active Directory-domänen

-   Matcha nätverksentiteter (användare, grupper och datorer)

-   Överföra relevanta data till Molntjänsten Azure ATP

-   Övervaka en enda domänkontrollant för en Azure ATP-sensorn eller övervaka flera domänkontrollanter från en enda fristående Azure ATP-sensorn.

Som standard stöder Azure ATP upp till 100 sensorer. Kontakta Azure ATP-supporten om du vill installera fler.

Fristående Azure ATP-sensorn tar emot nätverkstrafik och Windows-händelser från nätverket och bearbetar dessa i följande huvudkomponenter:

|||
|-|-|
|Nätverkslyssnare|Nätverkslyssnaren samlar in nätverkstrafik och Parsar trafiken. Det är aktiviteten kräver mycket processorkraft, så det är särskilt viktigt att kontrollera [Azure ATP krav](atp-prerequisites.md) när du planerar din Azure ATP-sensorn eller fristående Azure ATP-sensorn.|
|Händelselyssnare|Händelselyssnaren samlar in och Parsar Windows-händelser som vidarebefordras från en SIEM-server i nätverket.|
|Windows händelseloggläsare|Windows Händelseloggläsare läser och Parsar Windows-händelser som vidarebefordras till Azure ATP fristående sensorn Windows-händelselogg från domänkontrollanterna.|
|Nätverksaktivitetsöversättare | Översätter tolkad trafik till en logisk framställning av trafiken som används av Azure ATP (NetworkActivity).
|Entitetslösaren|Entitetslösaren tar tolkade data (nätverkstrafik och händelser) och löser dessa data med Active Directory för att hitta konto- och identitetsinformation. Den matchas sedan mot IP-adresser som finns i tolkade data. Entitetslösaren granskar paketrubriker på ett effektivt sätt för att möjliggöra tolkning av autentiseringspaket för datornamn, egenskaper och identiteter. Entitetslösaren kombinerar tolkade autentiseringspaket med data i det faktiska paketet.|
|Entitetssändare|Entitetssändaren skickar parsade och matchade data till Azure ATP-Molntjänsten.|

## <a name="azure-atp-sensor-features"></a>Funktioner i Azure ATP-sensorn

Följande funktioner fungerar på olika sätt beroende på om du har en Azure ATP-sensorn eller en fristående Azure ATP-sensorn.

-   Azure ATP-sensorn läser händelser lokalt, utan att behöva köpa och underhålla ytterligare maskinvara eller konfigurera vidarebefordran som krävs med ATP fristående sensorer. Azure ATP-sensorn har även stöd för tråd för Windows ETW (Event) som tillhandahåller logginformation för flera identifieringar. ETW baserat identifieringar omfattar både misstänkt replikering begära och befordran av domänkontrollant misstänkt, båda är den potentiella DCShadow attacker och stöds inte av ATP fristående sensorer.  

-   **Kandidat för domänsynkronisering**<br>
Kandidat för domänsynkronisering ansvarar för att proaktivt synkronisera alla entiteter från en specifik Active Directory-domän (liknar mekanismen som används av själva domänkontrollanterna för replikering). En sensor väljs slumpmässigt från listan över kandidater för att fungera som domänsynkroniserare. <br><br>
Om synkroniseraren är offline i mer än 30 minuter väljs en annan kandidat i stället. Om det finns någon domänsynkroniserare tillgänglig för en specifik domän, är Azure ATP proaktivt synkronisera entiteter och deras ändringar, men Azure ATP hämtar nya entiteter när de hittas i övervakad trafik. 
<br>Om det finns någon domänsynkroniserare tillgänglig och du söker efter en entitet som inte har någon trafik relaterad till den, visas inga sökresultat.<br><br>
Som standard synkroniseringskandidater alla Azure ATP fristående sensorer.<br><br>
Azure ATP-sensorer synkroniseringskandidater inte som standard.


-   **Resursbegränsningar**<br>
Azure ATP-sensorn innehåller en övervakningskomponent som utvärderar den tillgängliga beräknings- och minneskapaciteten på den domänkontrollant där den körs. Övervakningsprocessen körs var tionde sekund och uppdaterar dynamiskt processor- och minnesanvändningskvoten på processen för Azure ATP-sensorn att se till att domänkontrollanten vid en given tidpunkt har minst 15% lediga beräknings-och minnesresurser.<br><br>
Oavsett vad som händer på domänkontrollanten frigör den här processen alltid resurser för att se till att domänkontrollantens grundläggande funktioner inte påverkas.<br><br>
Om detta orsakar Azure ATP-sensorn till slut på resurser övervakas endast delvis trafik och övervakning varning ”förlorad portspeglad nätverkstrafik” visas på hälsosidan.

Följande tabell innehåller ett exempel på en domänkontrollant med tillräckligt med beräkningsresurser tillgängliga som möjliggör en större kvot än vad som krävs för närvarande, så att all trafik övervakas:

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Azure ATP-sensorn (Microsoft.Tri.sensor.exe)|Diverse (andra processer) |Azure ATP-sensorn kvot|Sensorn släpper trafik?|
|30 %|20 %|10 %|45 %|Nej|

Om Active Directory behöver mer bearbetningskraft, minskas kvoten som krävs av Azure ATP-sensorn. I följande exempel The Azure ATP-sensorn behöver mer än den tilldelade kvoten och släpper en del av trafiken (övervakar endast delvis trafik):

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Azure ATP-sensorn (Microsoft.Tri.sensor.exe)|Diverse (andra processer) |Azure ATP-sensorn kvot|Sensorn släpper trafik?|
|60%|15 %|10 %|15 %|Ja|


## <a name="your-network-components"></a>Dina nätverkskomponenter
Kontrollera att följande komponenter har ställts in, för att fungera med Azure ATP.

### <a name="port-mirroring"></a>Portspegling
Om du använder Azure ATP fristående sensorer, krävs portspegling set upp för de domänkontrollanter som övervakas. Ange Azure ATP-sensorn fristående som mål med hjälp av de fysiska eller virtuella växlarna. Ett annat alternativ är att använda nätverks-TAP. Azure ATP fungerar om vissa men inte alla domänkontrollanter övervakas, men identifieringar är mindre effektiva.

Även om portspegling speglar all domänkontrollantens nätverkstrafik till fristående Azure ATP-sensorn, det är bara en liten andel av denna trafik och sedan skickas i komprimerat format till Azure ATP molntjänst för analys.

Domänkontrollanterna och sensorer för Azure ATP-fristående kan vara fysiska eller virtuella. Mer information finns i [konfigurera portspegling](configure-port-mirroring.md).


### <a name="events"></a>händelser
För att förbättra Azure ATP-identifieringsomfattningen av Pass-the-Hash, misstänkt autentiseringsfel, ändring av känsliga grupper, skapande av misstänkt tjänster och Honey token aktivitetstyper av angrepp, Azure ATP-behov att analysera loggarna för följande Windows-händelser: 4776,4732,4733,4728,4729,4756,4757 och 7045. Dessa händelser läses automatiskt av Azure ATP-sensorer med rätt avancerade granskningsprinciper. I situationer där Azure ATP fristående sensorer har distribuerats, kan händelseloggarna vidarebefordras till den fristående sensorn på något av två olika sätt. Konfigurera Azure ATP-sensorn för fristående för att lyssna efter SIEM-händelser eller genom [konfigurera vidarebefordran av Windows händelser](configure-event-forwarding.md). 

> [!NOTE]
> - Windows-händelser vidarebefordran för fristående sensorer har inte stöd för ETW (Event Tracing för Windows). ETW baserat identifieringar omfattar både misstänkta replikeringsbegäran och misstänkta befordran av domänkontrollant, båda är den potentiella DCShadow attacker.  

-   Konfigurera Azure ATP-sensorn för fristående för att lyssna efter SIEM-händelser <br>Konfigurera SIEM för att vidarebefordra specifika Windows-händelser till ATP. Azure ATP stöder ett antal SIEM-leverantörer. Mer information finns i [konfigurera vidarebefordran av Windows händelser](configure-event-forwarding.md).

-   Konfigurera vidarebefordran av Windows-händelser<br>Du kan också Azure ATP kan även hämta händelser genom att konfigurera domänkontrollanterna så att de vidarebefordrar Windows-händelserna 4776, 4732, 4733, 4728, 4729, 4756, 4757 och 7045 till din Azure ATP fristående sensorn. Detta är särskilt användbart om du inte har en SIEM eller om din SIEM för närvarande inte stöds av ATP. Mer information om vidarebefordran av Windows händelser i ATP finns [konfigurera Windows-vidarebefordran](configure-event-forwarding.md). Detta gäller endast för fysiska Azure ATP fristående sensorer - inte till Azure ATP-sensorn.


## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-storleksverktyget](http://aka.ms/trisizingtool)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera vidarebefordran](configure-event-forwarding.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md)

- - [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
