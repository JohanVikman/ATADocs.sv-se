---
title: Azure Advanced Threat Protection-arkitektur | Microsoft Docs
description: "Här beskrivs arkitekturen i Azure Advanced Threat Analytics (ATP)"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/27/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ffa58d4e6ca24773f7168dd94ad0596878eaf151
ms.sourcegitcommit: 21d8f9abf909fc5f0e0da03cd100fa8fb950baa4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/27/2018
---
*Gäller för: Azure Advanced Threat Protection*


# <a name="azure-atp-architecture"></a>Azure ATP-arkitektur
Azure Advanced Threat Protection-arkitekturen beskrivs i det här diagrammet:

![Topologidiagram för Azure ATP-arkitektur](media/atp-architecture-topology.png)

Azure ATP övervakar dina domänkontrollantens nätverkstrafik genom att använda portspegling till en Azure ATP fristående sensor använder fysiska eller virtuella växlar. Om du distribuerar Azure ATP-sensor direkt på domänkontrollanterna undanröjer behovet för portspegling. Azure ATP kan dessutom dra nytta av Windows-händelser (vidarebefordras direkt från domänkontrollanterna eller från en SIEM-server) och analysera data beträffande attacker och hot. Azure ATP tar emot tolkad trafik från Azure ATP fristående sensor och Azure ATP sensor. Därefter genomför tjänsten profilering, kör deterministisk identifiering, och kör maskininlärnings- och beteendealgoritmer för att lära sig om ditt nätverk, identifierar avvikelser samt varnar dig för misstänkta aktiviteter.

Det här avsnittet beskriver flödet i nätverk och händelseinsamling och beskriver funktionerna för huvudkomponenterna i ATP: Azure ATP fristående sensor, Azure ATP-temperatursensor (som har samma grundfunktioner som Azure ATP fristående sensor) och Azure ATP-Molntjänsten. 

## <a name="azure-atp-components"></a>Azure ATP-komponenter
Azure ATP består av följande komponenter:

-   **Azure-hanteringsportalen för ATP arbetsytan** <br>
Hanteringsportalen för Azure ATP arbetsytan kan du skapa arbetsytor och möjliggör integrering med andra Microsoft-tjänster.

> [!NOTE]
> Endast sensorer från en enda Active Directory-skog kan ansluta till en enda arbetsyta.

-   **Azure portal för ATP-arbetsytan** <br>
Azure ATP arbetsytan portal tar emot data från ATP sensorer och fristående sensorer. Övervakar, hanterar och undersöker hoten i din miljö.

-   **Azure ATP-temperatursensor**<br>
Azure ATP-temperatursensor installeras direkt på domänkontrollanterna och övervakar trafiken direkt, utan att behöva en dedikerad server eller konfiguration av portspegling. 

-   **Azure ATP fristående sensor**<br>
Azure ATP fristående sensorn har installerats på en dedikerad server som övervakar trafiken från domänkontrollanterna med antingen portspegling eller en nätverks-TAP. Det är ett alternativ till Azure ATP sensorn.

## <a name="deployment-options"></a>Distributionsalternativ
Du kan distribuera Azure ATP med följande kombination av sensorer:

-   **Med hjälp av endast Azure ATP sensorer**<br>
Distributionen av Azure ATP kan innehålla endast Azure ATP sensorer: I Azure ATP sensorer distribueras på varje domänkontrollant och inga ytterligare servrar eller konfiguration av portspegling krävs.

-   **Med hjälp av endast Azure ATP fristående sensorer** <br>
Distributionen av Azure ATP kan innehålla endast Azure ATP fristående sensorer, utan någon Azure ATP sensorer: alla domänkontrollanter måste konfigureras för att aktivera portspegling till en fristående Azure ATP-sensor eller nätverks-TAP måste vara på plats.

-   **Med hjälp av Azure ATP sensorer och Azure ATP fristående sensorer**<br>
Azure ATP distributionen omfattar både Azure ATP fristående sensorer och Azure ATP sensorer. Azure ATP sensorer är installerade på vissa av dina domänkontrollanter (till exempel alla domänkontrollanter hos avdelningskontor). På samma gång övervakas andra domänkontrollanter av Azure ATP fristående sensorer (till exempel de större domänkontrollanterna i huvuddatacentren).


### <a name="azure-atp-workspace-management-portal"></a>Azure-hanteringsportalen för ATP arbetsytan

Hanteringsportalen för Azure ATP arbetsytan kan du:

-   Skapa och hantera Azure ATP arbetsytor

-   Integrera med andra Microsoft-säkerhetstjänster

Ange huvudsakliga arbetsytan som **primära**. Endast en arbetsyta kan anges som primär. Ange en arbetsyta som primär effekter integreringar - kan du endast integrera Azure ATP med Windows Defender ATP för den primära arbetsytan. Du kan ändra vilken arbetsyta är primära senare, men för att kunna göra så du måste ta bort alla integreringar som redan angetts för den aktuella primära arbetsytan.

> [!NOTE]
> Azure ATP stöder för närvarande skapandet av två arbetsytor. Vi rekommenderar att du skapar en primära arbetsytan för produktionsmiljön och en ytterligare arbetsyta som en fristående miljö.

### <a name="azure-atp-workspace-portal"></a>Azure portal för ATP-arbetsytan

Arbetsytan Azure ATP kan du hantera Azure ATP följande funktioner:

-   Hantera Azure ATP sensor och fristående sensor konfigurationsinställningar

-   Visa data från Azure ATP fristående sensorer och Azure ATP sensorer 

-   Övervakaren upptäckte misstänkta aktiviteter baserat på användarbeteende maskininlärningsalgoritmer för att identifiera onormalt beteende och deterministiska algoritmer för att identifiera avancerade attacker baserat på attackkedjan

-   Valfritt: hanteringsportalen arbetsytan konfigureras för att skicka e-post och händelser när misstänkta aktiviteter eller hälsa händelser identifieras.


|||
|-|-|
|Entitetsmottagare|Tar emot entitetsgrupper från alla Azure ATP sensorer och Azure ATP fristående sensorer.|
|Nätverksaktivitetsprocessor|Bearbetar alla nätverksaktiviteter inom varje grupp som tas emot. Till exempel utförs matchning mellan de olika Kerberos-stegen från potentiellt olika datorer|
|Entitetsprofilerare|Profilerar alla unika entiteter enligt trafik och händelser. Till exempel uppdaterar Azure ATP listan över inloggade datorer för varje användarprofil.|
|Azure-hanteringsportalen för ATP arbetsytan|Hanterar dina Azure ATP arbetsytor.|
|Azure portal för ATP-arbetsytan|Arbetsytan Azure ATP används för att konfigurera Azure ATP och övervaka misstänkta aktiviteter som identifieras av Azure ATP på nätverket. Arbetsytan Azure ATP är inte beroende av Azure ATP-sensor och körs även när tjänsten Azure ATP sensorn har stoppats. |
|Detektorer|Detektorerna använder maskininlärningsalgoritmer och deterministiska regler för att hitta misstänkta aktiviteter och onormalt användarbeteende i nätverket.|

Överväg följande villkor när du bestämmer hur många Azure ATP arbetsytor du distribuerar i nätverket:

-   En Azure ATP arbetsytan kan övervaka en Active Directory-skog. Om du har mer än en Active Directory-skog, måste minst en tjänst i Azure ATP molnet per Active Directory-skog.


## <a name="azure-atp-sensor-and-azure-atp-standalone-sensor"></a>Azure ATP sensor och Azure ATP fristående sensor

Den **Azure ATP sensor** och **Azure ATP sensor** har båda samma grundläggande funktioner:

-   Samla in och inspektera nätverkstrafik på domänkontrollanter. Detta är portspeglad trafik för Azure ATP fristående sensorer och lokal trafik på domänkontrollanten i Azure ATP sensorer. 

-   Ta emot Windows-händelser direkt från domänkontrollanterna (för ATP sensorer) eller från SIEM- eller Syslog-servrar (för ATP fristående sensorer)

-  Ta emot RADIUS-redovisningsinformation från din VPN-leverantör

-   Hämta information om användare och datorer från Active Directory-domänen

-   Matcha nätverksentiteter (användare, grupper och datorer)

-   Överföra relevanta data till Molntjänsten Azure ATP

-   Övervaka flera domänkontrollanter från en enda Azure ATP fristående sensor eller övervaka en enda domänkontrollant för en Azure ATP sensor.

Azure ATP fristående sensor tar emot nätverkstrafik och Windows-händelser från nätverket och bearbetar dessa i följande huvudkomponenter:

|||
|-|-|
|Nätverkslyssnare|Nätverkslyssnaren avbildas nätverkstrafik och Parsar trafiken. Det här är en aktivitet processorkraft, så det är särskilt viktigt att kontrollera [Azure ATP krav](atp-prerequisites.md) när du planerar din Azure ATP-sensor eller Azure ATP fristående sensor.|
|Händelselyssnare|Den Händelselyssnaren avbildas och tolkar Windows-händelser som vidarebefordras från en SIEM-server i nätverket.|
|Windows händelseloggläsare|Windows Händelseloggläsare läser och tolkar Windows-händelser som vidarebefordras i Azure ATP fristående sensor Windows-händelselogg från domänkontrollanterna.|
|Nätverksaktivitetsöversättare | Översätter tolkad trafik till en logisk framställning av trafiken som används av Azure ATP (NetworkActivity).
|Entitetslösaren|Entitetslösaren tar tolkade data (nätverkstrafik och händelser) och löser dessa data med Active Directory för att hitta konto- och identitetsinformation. Den matchas sedan mot IP-adresser som finns i tolkade data. Entitetslösaren granskar paketrubriker på ett effektivt sätt för att möjliggöra tolkning av autentiseringspaket för datornamn, egenskaper och identiteter. Entitetslösaren kombinerar tolkade autentiseringspaket med data i det faktiska paketet.|
|Entitetssändare|Entitetssändaren skickar tolkade och matchade data till Azure ATP-Molntjänsten.|

## <a name="azure-atp-sensor-features"></a>Azure ATP sensor-funktioner

Följande funktioner fungerar på olika sätt beroende på om du använder en fristående Azure ATP-sensor eller en Azure ATP sensor.

-   Azure ATP-sensor kan läsa händelser lokalt, utan att behöva konfigurera vidarebefordran av händelser.

-   **Kandidat för domänsynkronisering**<br>
Kandidat för domänsynkronisering ansvarar för att proaktivt synkronisera alla entiteter från en specifik Active Directory-domän (liknar mekanismen som används av själva domänkontrollanterna för replikering). En sensor väljs slumpmässigt från listan över kandidater för att fungera som domänsynkroniserare. <br><br>
Om synkroniseraren är offline i mer än 30 minuter väljs en annan kandidat i stället. Om det finns någon domänsynkroniserare tillgänglig för en specifik domän, är Azure ATP kunna synkronisera entiteter och deras ändringar proaktivt men Azure ATP hämtar nya entiteter när de hittas i övervakad trafik. 
<br>Om det inte finns någon domänsynkroniserare, och du söker efter en entitet som inte har någon trafik relaterad till den, visas inga sökresultat.<br><br>
Som standard synkroniseringskandidater alla Azure ATP fristående sensorer.<br><br>
Azure ATP sensorer synkroniseringskandidater inte som standard.


-   **Resursbegränsningar**<br>
Azure ATP-sensor innehåller en övervakningskomponent som utvärderar den tillgängliga kapaciteten för beräknings- och minneskapaciteten på den domänkontrollant där den körs. Övervakningsprocessen körs var 10: e sekund och uppdaterar dynamiskt processor- och minnesanvändningskvoten på Azure ATP sensor processen för att se till att domänkontrollanten vid varje given tidpunkt har minst 15% lediga beräknings- och minnesresurser.<br><br>
Oavsett vad som händer på domänkontrollanten frigör den här processen alltid resurser för att se till att domänkontrollantens grundläggande funktioner inte påverkas.<br><br>
Om detta orsakar Azure ATP sensor till slut på resurser övervakas endast delar av trafiken och den övervakning aviseringen ”bort portspeglad nätverkstrafik” visas på hälsosidan.

Följande tabell innehåller ett exempel på en domänkontrollant med tillräckligt med beräkningsresurser tillgängliga som möjliggör en större kvot än vad som krävs för närvarande, så att all trafik övervakas:

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Azure ATP temperatursensor (Microsoft.Tri.sensor.exe)|Diverse (andra processer) |Azure ATP sensor kvot|Släpper sensor trafik?|
|30 %|20 %|10 %|45 %|Nej|

Om Active Directory behöver mer datorkraft, minskas kvoten som krävs av Azure ATP sensorn. I följande exempel i Azure ATP sensor behöver mer än den tilldelade kvoten och släpper en del av trafiken (övervakar endast delvis trafik):

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Azure ATP temperatursensor (Microsoft.Tri.sensor.exe)|Diverse (andra processer) |Azure ATP sensor kvot|Släpper sensor trafik?|
|60%|15 %|10 %|15 %|Ja|


## <a name="your-network-components"></a>Dina nätverkskomponenter
Se till att kontrollera att följande komponenter har ställts in för att fungera med Azure ATP.

### <a name="port-mirroring"></a>Portspegling
Om du använder Azure ATP fristående sensorer som du behöver konfigurera portspegling för de domänkontrollanter som övervakas och ange Azure ATP fristående sensor som mål med hjälp av de fysiska eller virtuella växlarna. Ett annat alternativ är att använda nätverks-TAP. Azure ATP fungerar om vissa men inte alla domänkontrollanter övervakas, men identifieringar är mindre effektiva.

Även om portspegling speglar all domänkontrollantens nätverkstrafik till Azure ATP fristående sensor, är en liten andel av denna trafik och sedan skickas i komprimerat format till Azure-ATP Molntjänsten för analys.

Domänkontrollanterna och Azure ATP fristående sensorer kan vara fysiska eller virtuella. Mer information finns i [konfigurera portspegling](configure-port-mirroring.md).


### <a name="events"></a>händelser
Om du vill förbättra Azure ATP-identifieringen av Pass-the-Hash, Brute Force, ändring av känsliga grupper, skapande av misstänkt tjänster, ändringar av honung token Azure ATP måste följande Windows-händelser: 4776, 4732, 4733, 4728, 4729, 4756, 4757 och 7045. Dessa kan antingen läsas automatiskt av Azure ATP-sensor eller om Azure ATP-sensor inte har distribuerats, den kan vidarebefordras till Azure ATP fristående sensor i ett av två sätt, genom att konfigurera fristående Azure ATP sensorn så att den lyssnar efter SIEM-händelser eller genom att [Konfigurera vidarebefordran av Windows-händelse](configure-event-forwarding.md).

-   Konfigurera Azure ATP fristående sensor så att den lyssnar efter SIEM-händelser <br>Konfigurera SIEM för att vidarebefordra specifika Windows-händelser till ATP. Azure ATP stöder ett antal SIEM-leverantörer. Mer information finns i [konfigurera vidarebefordran av händelser](configure-event-forwarding.md).

-   Konfigurera vidarebefordran av Windows-händelser<br>Du kan också Azure ATP kan även hämta händelser genom att konfigurera domänkontrollanterna så att de vidarebefordrar Windows-händelser 4776, 4732, 4733, 4728, 4729, 4756, 4757 och 7045 till din Azure ATP fristående sensor. Detta är särskilt användbart om du inte har en SIEM eller om din SIEM för närvarande inte stöds av ATP. Mer information om vidarebefordran av Windows-händelse i ATP finns [Konfigurera händelse vidarebefordran av Windows](configure-event-forwarding.md). Detta gäller endast fysiska Azure ATP fristående sensorer - inte till Azure ATP-sensor.


## <a name="see-also"></a>Se även
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-storleksverktyget](http://aka.ms/trisizingtool)
- [Azure ATP-kapacitetsplanering](atp-capacity-planning.md)
- [Konfigurera vidarebefordran av händelser](configure-event-forwarding.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-forwarding.md)

- - [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)
