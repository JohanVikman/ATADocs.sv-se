---
title: Advanced Threat Analytics-arkitektur | Microsoft Docs
description: Beskriver arkitekturen i Microsoft Advance Threat Analytics (ATA)
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b620e5b6203d387de389cfb857c2dd6125239ed9
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010065"
---
*Gäller för: Advanced Threat Analytics version 1.9.*




# <a name="ata-architecture"></a>ATA-arkitektur
Arkitekturen för Advanced Threat Analytics beskrivs i det här diagrammet:

![Topologidiagram för ATA-arkitekturen](media/ATA-architecture-topology.jpg)

ATA övervakar nätverkstrafiken på dina domänkontrollanter genom att använda portspegling mot en ATA-gateway med fysiska eller virtuella växlar. Om du distribuerar ATA Lightweight Gateway direkt på domänkontrollanterna krävs inte portspegling. Dessutom kan ATA utnyttja Windows-händelser (vidarebefordras direkt från domänkontrollanterna eller en SIEM-server) och analysera data beträffande attacker och hot.
Det här avsnittet beskriver nätverkstrafik- och händelseinsamlingsflödet samt huvudkomponenterna i ATA: ATA Gateway, ATA Lightweight Gateway (som har samma grundfunktioner som ATA Gateway) och ATA Center.


![Trafikflödesdiagram för ATA](media/ATA-traffic-flow.jpg)

## <a name="ata-components"></a>ATA-komponenter
ATA består av följande komponenter:

-   **ATA Center** <br>
ATA Center tar emot data från ATA-gatewayer och/eller ATA Lightweight-gatewayer som du distribuerar.
-   **ATA Gateway**<br>
ATA Gateway installeras på en dedikerad server som övervakar trafiken från domänkontrollanterna med antingen portspegling eller en nätverks-TAP.
-   **ATA Lightweight Gateway**<br>
ATA Lightweight Gateway installeras direkt på domänkontrollanterna och övervakar trafiken direkt, utan att behöva en dedikerad server eller konfiguration av portspegling. Det är ett alternativ till ATA Gateway.

En ATA-distribution kan bestå av ett enda ATA Center som är anslutet till alla ATA-gatewayer, alla ATA Lightweight-gatewayer eller en kombination av ATA-gatewayer och ATA Lightweight-gatewayer.


## <a name="deployment-options"></a>Distributionsalternativ
Du kan distribuera ATA med följande kombination av gatewayer:

-   **Endast med ATA Gateway** <br>
ATA-distributionen kan innehålla endast ATA-gatewayer, utan några ATA Lightweight-gatewayer: Alla domänkontrollanter måste konfigureras för portspegling mot en ATA-gateway, alternativt krävs nätverks-TAP.
-   **Endast med ATA Lightweight Gateway**<br>
ATA-distributionen kan innehåller endast ATA Lightweight-gatewayer: ATA Lightweight-gatewayerna distribueras på varje domänkontrollant och inga ytterligare servrar eller konfiguration av portspegling krävs.
-   **Med både ATA Gateway och ATA Lightweight Gateway**<br>
ATA-distributionen omfattar både ATA-gatewayer och ATA Lightweight-gatewayer. ATA Lightweight-gatewayerna installeras på vissa av dina domänkontrollanter (till exempel alla domänkontrollanter på dina förgreningsplatser). Samtidigt övervakas andra domänkontrollanter av ATA-gatewayer (till exempel de större domänkontrollanterna på huvuddatacenter).

I alla dessa scenarier skickar alla gatewayer sina data till ATA Center.




## <a name="ata-center"></a>ATA Center
**ATA Center** utför följande funktioner:

-   Hanterar konfigurationsinställningar för ATA Gateway och ATA Lightweight Gateway

-   Tar emot data från ATA-gatewayer och ATA Lightweight-gatewayer 

-   Identifierar misstänkta aktiviteter

-   Kör ATA-maskininlärningsalgoritmer för beteende för att upptäcka onormalt beteende

-   Kör olika deterministiska algoritmer för att identifiera avancerade attacker baserat på attackkedjan

-   Kör ATA-konsolen

-   Valfritt: ATA Center kan konfigureras för att skicka e-post och händelser när en misstänkt aktivitet upptäcks.

ATA Center tar emot parsad trafik från ATA Gateway och ATA Lightweight Gateway. Därefter genomför tjänsten profilering, kör deterministisk identifiering, och kör maskininlärnings- och beteendealgoritmer för att lära sig om ditt nätverk, identifierar avvikelser samt varnar dig för misstänkta aktiviteter.

|||
|-|-|
|Entitetsmottagare|Tar emot grupper med entiteter från alla ATA-gatewayer och ATA Lightweight-gatewayer.|
|Nätverksaktivitetsprocessor|Bearbetar alla nätverksaktiviteter inom varje grupp som tas emot. Till exempel utförs matchning mellan de olika Kerberos-stegen från potentiellt olika datorer|
|Entitetsprofilerare|Profilerar alla unika entiteter enligt trafik och händelser. Till exempel uppdaterar ATA listan över inloggade datorer för varje användarprofil.|
|Centerdatabas|Hanterar skrivprocessen för nätverksaktiviteter och händelser till databasen. |
|Databas|ATA använder MongoDB för lagring av alla data i systemet:<br /><br />– Nätverksaktiviteter<br />– Händelseaktiviteter<br />– Unika entiteter<br />– Misstänkta aktiviteter<br />– ATA-konfiguration|
|Detektorer|Detektorerna använder maskininlärningsalgoritmer och deterministiska regler för att hitta misstänkta aktiviteter och onormalt användarbeteende i nätverket.|
|ATA-konsolen|ATA-konsolen används för att konfigurera ATA och övervaka misstänkta aktiviteter som identifieras av ATA i nätverket. ATA-konsolen är inte beroende av ATA Center-tjänsten och körs även om tjänsten har stoppats, förutsatt att den kan kommunicera med databasen.|
Tänk på följande när du bestämmer hur många ATA Center som ska distribueras i nätverket:

-   Ett ATA Center kan övervaka en enda Active Directory-skog. Om du har fler än en Active Directory-skog behöver du minst ett ATA Center per Active Directory-skog.

-    I stora Active Directory-distributioner kanske inte ett enda ATA Center kan hantera all trafik på alla domänkontrollanter. I så fall krävs flera ATA Center. Antalet ATA Center bör avgöras genom [ATA-kapacitetsplanering](ata-capacity-planning.md).

## <a name="ata-gateway-and-ata-lightweight-gateway"></a>ATA Gateway och ATA Lightweight Gateway

### <a name="gateway-core-functionality"></a>Grundläggande funktioner för gateway
**ATA Gateway** och **ATA Lightweight Gateway** har båda samma grundläggande funktioner:

-   Samla in och inspektera nätverkstrafik på domänkontrollanter. Det här är portspeglad trafik för ATA-gatewayer och lokal trafik för domänkontrollanten i ATA Lightweight-gatewayer. 

-   Ta emot Windows-händelser från SIEM- eller Syslog-servrar eller från domänkontrollanter med hjälp av vidarebefordran av Windows-händelser

-   Hämta information om användare och datorer från Active Directory-domänen

-   Matcha nätverksentiteter (användare, grupper och datorer)

-   Överföra relevanta data till ATA Center

-   Övervaka flera domänkontrollanter från en enda ATA Gateway eller övervaka en enskild domänkontrollant för ATA Lightweight Gateway.

ATA Gateway tar emot nätverkstrafik och Windows-händelser från nätverket och bearbetar dessa i följande huvudkomponenter:

|||
|-|-|
|Nätverkslyssnare|Nätverkslyssnaren samlar in nätverkstrafik och parsar trafiken. Den här aktiviteten kräver mycket processorkraft, så det är särskilt viktigt att kontrollera [Krav för ATA](ata-prerequisites.md) när du planerar för ATA Gateway och ATA Lightweight Gateway.|
|Händelselyssnare|Händelselyssnaren samlar in och parsar Windows-händelser som vidarebefordras från en SIEM-server i ditt nätverk.|
|Windows händelseloggläsare|Windows-händelseloggläsaren läser och parsar Windows-händelser som vidarebefordras till ATA-gatewayens Windows-händelselogg från domänkontrollanterna.|
|Nätverksaktivitetsöversättare | Översätter tolkad trafik till en logisk återgivning av trafiken som används av ATA (NetworkActivity).
|Entitetslösaren|Entitetslösaren tar tolkade data (nätverkstrafik och händelser) och löser dessa data med Active Directory för att hitta konto- och identitetsinformation. Den matchas sedan mot IP-adresser som finns i tolkade data. Entitetslösaren granskar paketrubriker på ett effektivt sätt för att möjliggöra tolkning av autentiseringspaket för datornamn, egenskaper och identiteter. Entitetslösaren kombinerar tolkade autentiseringspaket med data i det faktiska paketet.|
|Entitetssändare|Entitetssändaren skickar parsade och matchade data till ATA Center.|

## <a name="ata-lightweight-gateway-features"></a>Funktioner för ATA Lightweight Gateway

Följande funktioner fungerar på olika sätt beroende på om du kör ATA Gateway eller ATA Lightweight Gateway.

-   ATA Lightweight Gateway kan läsa händelser lokalt, utan att du behöver konfigurera vidarebefordran av händelser.

-   **Kandidat för domänsynkronisering**<br>
Domänsynkroniseringsgateway ansvarar för att proaktivt synkronisera alla entiteter från en specifik Active Directory-domän (liknar mekanismen som används av själva domänkontrollanterna för replikering). En gateway väljs slumpmässigt från listan över kandidater för att fungera som domänsynkroniserare. <br><br>
Om synkroniseraren är offline i mer än 30 minuter väljs en annan kandidat i stället. Om det finns någon domänsynkroniserare tillgänglig för en specifik domän, är ATA synkronisera entiteter och deras ändringar proaktivt men ATA kan reaktivt hämta nya entiteter när de hittas i övervakad trafik. 
<br>Om det inte finns någon domänsynkroniserare, och du söker efter en entitet som inte har någon trafik relaterad till den, visas inga sökresultat.<br><br>
Som standard är alla ATA-gatewayer synkroniseringskandidater.<br><br>
Eftersom alla ATA Lightweight-gatewayer mer troligt distribueras på avdelningskontor och på små domänkontrollanter är de som standard inte synkroniseringskandidater.


-   **Resursbegränsningar**<br>
ATA Lightweight Gateway innehåller en övervakningskomponent som utvärderar den tillgängliga kapaciteten för beräknings- och minneskapaciteten på den domänkontrollant där den körs. Övervakningsprocessen körs var 10:e sekund och uppdaterar dynamiskt processor- och minnesanvändningskvoten på ATA Lightweight Gateway-processen för att se till att domänkontrollanten vid varje given tidpunkt har minst 15 % lediga beräknings- och minnesresurser.<br><br>
Oavsett vad som händer på domänkontrollanten frigör den här processen alltid resurser för att se till att domänkontrollantens grundläggande funktioner inte påverkas.<br><br>
Om detta orsakar ATA Lightweight Gateway får slut på resurser övervakas endast delar av trafiken och den övervakning aviseringen ”bort portspeglad nätverkstrafik” visas på hälsosidan.

Följande tabell innehåller ett exempel på en domänkontrollant med tillräckligt med beräkningsresurser tillgängliga som möjliggör en större kvot än vad som krävs för närvarande, så att all trafik övervakas:

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA Lightweight Gateway (Microsoft.Tri.Gateway.exe)|Diverse (andra processer) |Kvot för ATA Lightweight Gateway|Släppt av gateway|
|30 %|20 %|10 %|45 %|Nej|

Om Active Directory behöver mer beräkning minskas kvoten som krävs av ATA Lightweight Gateway. I följande exempel behöver ATA Lightweight Gateway mer än den tilldelade kvoten och släpper en del av trafiken (övervakar endast delvis trafik):

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA Lightweight Gateway (Microsoft.Tri.Gateway.exe)|Diverse (andra processer) |Kvot för ATA Lightweight Gateway|Släpper gateway|
|60 %|15 %|10 %|15 %|Ja|


## <a name="your-network-components"></a>Dina nätverkskomponenter
Se till att kontrollera att följande komponenter har ställts in för att arbeta med ATA.

### <a name="port-mirroring"></a>Portspegling
Om du använder ATA-gatewayer behöver du konfigurera portspegling för de domänkontrollanter som övervakas och ange ATA Gateway som mål med hjälp av de fysiska eller virtuella växlarna. Ett annat alternativ är att använda nätverks-TAP. ATA fungerar om vissa men inte alla domänkontrollanter övervakas, men identifieringar är mindre effektiva.

Även om portspegling speglar all domänkontrollantstrafik till ATA Gateway är endast en liten andel av denna trafik som sedan skickas i komprimerat format till ATA Center för analys.

Domänkontrollanterna och ATA-gatewayerna kan vara fysiska eller virtuella, mer information finns i [Konfigurera portspegling](configure-port-mirroring.md).


### <a name="events"></a>händelser
Om du vill förbättra ATA-identifieringen av Pass-the-Hash, Brute Force, Ändring av känsliga grupper och Honey tokens behöver ATA följande Windows-händelser: 4776, 4732, 4733, 4728, 4729, 4756, 4757. Dessa kan antingen läsas automatiskt av ATA Lightweight Gateway eller, om ATA Lightweight Gateway inte har distribuerats, vidarebefordras till ATA Gateway på något av två sätt genom att ATA Gateway konfigureras att lyssna efter SIEM-händelser eller genom att [vidarebefordran av Windows-händelser konfigureras](#configuring-windows-event-forwarding).

-   Konfigurera ATA Gateway för att lyssna efter SIEM-händelser <br>Konfigurera SIEM för att vidarebefordra specifika Windows-händelser till ATA. ATA har stöd för ett antal SIEM-leverantörer. Mer information finns i [Konfigurera händelseinsamling](configure-event-collection.md).

-   Konfigurera vidarebefordran av Windows-händelser<br>Du kan också ATA kan även hämta händelser genom att konfigurera domänkontrollanterna så att de vidarebefordrar Windows-händelser 4776, 4732, 4733, 4728, 4729, 4756 och 4757 till ATA Gateway. Det här är särskilt användbart om du inte har en SIEM eller om din SIEM för närvarande inte stöds av ATA. Mer information om vidarebefordran av Windows-händelser i ATA finns i [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding). Detta gäller endast för fysisk ATA-gatewayer - inte till ATA Lightweight Gateway.

## <a name="related-videos"></a>Relaterade videor
- [Välja rätt ATA Gateway-typ](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-storleksverktyget](http://aka.ms/atasizingtool)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

