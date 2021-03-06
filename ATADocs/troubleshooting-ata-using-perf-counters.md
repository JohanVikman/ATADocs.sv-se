---
title: Felsök Advanced Threat Analytics med prestandaräknare | Microsoft Docs
description: Beskriver hur du kan använda prestandaräknare för att felsöka problem med ATA
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: df162a62-f273-4465-9887-94271f5000d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 455e66b286916f125fcc34d61b167b86ccc59740
ms.sourcegitcommit: caaa864708ec631ca4903f6270ad0012951ceef1
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/25/2018
ms.locfileid: "47114467"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="troubleshooting-ata-using-the-performance-counters"></a>Felsöka ATA med prestandaräknarna
ATA-prestandaräknarna ger information om hur bra varje komponent i ATA fungerar. Komponenterna i ATA bearbetar data i tur och ordning. Om ett problem uppstår kan det därför leda till förlorad trafik någonstans i komponentkedjan. För att åtgärda problemet måste du ta reda på vilken komponent som krånglar och åtgärda problemet i början av kedjan. Använd data i prestandaräknarna för att förstå hur varje komponent fungerar.
Mer information om flödet av interna ATA-komponenter finns i [ATA-arkitektur](ata-architecture.md).

**Process för ATA-komponenter**:

1.  När en komponent når maximal storlek blockerar den föregående komponent från att skicka fler entiteter till den.

2.  Slutligen börjar föregående komponent öka **sin** egen storlek tills den blockerar komponenten före den från att skicka fler entiteter.

3.  Detta inträffar ända tillbaka till NetworkListener-komponenten som förlorar trafik när den inte längre kan vidarebefordra entiteter.


## <a name="retrieving-performance-monitor-files-for-troubleshooting"></a>Hämta prestandaövervakningsfiler för felsökning

Så här hämtar du prestandaövervakningsfilerna (BLG) från de olika ATA-komponenterna:
1.  Öppna perfmon.
2.  Stoppa datainsamlaruppsättningen namngivna: **Microsoft ATA Gateway** eller **Microsoft ATA Center**.
3.  Gå till mappen för datainsamlaruppsättningen (som standard är det ”C:\Program Files\Microsoft Advanced Threat Analytics\Gateway\Logs\DataCollectorSets” eller ”C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs\DataCollectorSets”).
4.  Kopiera den BLG-fil som senast ändrades.
5.  Starta om datainsamlaruppsättningen namngivna: **Microsoft ATA Gateway** eller **Microsoft ATA Center**.


## <a name="ata-gateway-performance-counters"></a>Prestandaräknare i ATA Gateway

I det här avsnittet avser varje hänvisning till ATA Gateway också ATA Lightweight Gateway.

Du kan prestandatillståndet i realtid för ATA Gateway genom att lägga till ATA-gatewayens prestandaräknare.
Detta görs genom att öppna **Prestandaövervakaren** och lägga till alla räknare för ATA Gateway. Namnet på prestandaräknarobjektet är: **Microsoft ATA Gateway**.

Här är listan med de viktigaste ATA Gateway-räknarna som du bör vara medveten om:

> [!div class="mx-tableFixed"]
|Räknare|Beskrivning|Tröskelvärde|Felsökning|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Gateway\NetworkListener PEF parsade meddelanden\Sek|Mängden trafik som bearbetas av ATA Gateway varje sekund.|Inget tröskelvärde|Hjälper dig att förstå mängden trafik som parsas av ATA Gateway.|
|NetworkListener PEF – förlorade händelser/s|Mängden trafik som förloras av ATA Gateway varje sekund.|Det här antalet bör alltid vara noll (sällsynta korta förekomster av förlorade meddelanden är godtagbara).|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|Microsoft ATA Gateway\NetworkListener – ETW-ignorerade händelser/s|Mängden trafik som förloras av ATA Gateway varje sekund.|Det här antalet bör alltid vara noll (sällsynta korta förekomster av förlorade meddelanden är godtagbara).|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|Microsoft ATA Gateway\NetworkActivityTranslator – blockstorlek för meddelandedatanummer|Mängden trafik i kö för översättning till nätverksaktiviteter (NA).|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 100 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|Microsoft ATA Gateway\EntityResolver – blockstorlek för aktivitet|Antal Nätverksaktiviteter (na) i kö för matchning.|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 10 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|Microsoft ATA Gateway\EntitySender – blockstorlek för entitetsbatch|Antal nätverksaktiviteter (NA) i kö för att skickas till ATA Center.|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 1 000 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|Microsoft ATA Gateway\EntitySender – sändningstid för batch|Tiden det tog att skicka den senaste batchen.|Bör oftast vara mindre än 1 000 millisekunder|Kontrollera om det finns några nätverksproblem mellan ATA Gateway och ATA Center.|

> [!NOTE]
> -   Tidsinställda räknare anges i millisekunder.
> -   Ibland är det mer praktiskt att övervaka den fullständiga listan med räknare med hjälp av den **rapporten** graph typ (exempel: realtidsövervakning av alla räknare)

## <a name="ata-lightweight-gateway-performance-counters"></a>ATA Lightweight Gateway-prestandaräknare
Prestandaräknare kan användas för kvothantering i Lightweight Gateway, för att se till att ATA inte tömmer för många resurser från domänkontrollanter som har installerats.
För att mäta de resursbegränsningar som ATA framtvingar på Lightweight-gatewayen, lägger du till de här räknarna.

Detta görs genom att öppna **Prestandaövervakaren** och lägga till alla räknare för ATA Lightweight Gateway. Namnen på prestandaräknarna är: **Microsoft ATA Gateway** och **Microsoft ATA Gateway Updater**.

> [!div class="mx-tableFixed"]
|Räknare|Beskrivning|Tröskelvärde|Felsökning|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager maximal processortid i %|Den maximala mängden processortid (i procent) som Lightweight Gateway-processen kan använda. |Inget tröskelvärde. | Detta är den begränsning som skyddar domänkontrollantresurserna från att användas av ATA Lightweight Gateway. Om du ser att processen ofta når gränsen under en tidsperiod (processen når gränsen och börjar sedan att släppa trafik) innebär det att du måste lägga till fler resurser på servern som kör domänkontrollanten.|
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager dedikera maximal minnesstorlek|Den maximala mängden dedikerat minne (i byte) som Lightweight Gateway-processen kan använda.|Inget tröskelvärde. | Detta är den begränsning som skyddar domänkontrollantresurserna från att användas av ATA Lightweight Gateway. Om du ser att processen ofta når gränsen under en tidsperiod (processen når gränsen och börjar sedan att släppa trafik) innebär det att du måste lägga till fler resurser på servern som kör domänkontrollanten.| 
|Microsoft ATA Gateway Updater\GatewayUpdaterResourceManager storleksgräns för arbetsminne|Den maximala mängden fysiskt minne (i byte) som Lightweight Gateway-processen kan använda.|Inget tröskelvärde. | Detta är den begränsning som skyddar domänkontrollantresurserna från att användas av ATA Lightweight Gateway. Om du ser att processen ofta når gränsen under en tidsperiod (processen når gränsen och börjar sedan att släppa trafik) innebär det att du måste lägga till fler resurser på servern som kör domänkontrollanten.|



Om du vill se din faktiska användning, se följande räknare:


> [!div class="mx-tableFixed"]
|Räknare|Beskrivning|Tröskelvärde|Felsökning|
|-----------|---------------|-------------|-------------------|
|Process(Microsoft.Tri.gateway)\%processortid|Mängden processortid (i procent) som Lightweight Gateway-processen faktiskt använder. |Inget tröskelvärde. | Jämför resultatet från den här räknaren med gränsen i maximal processortid i % för GatewayUpdaterResourceManager. Om du ser att processen ofta når gränsen under en tidsperiod (processen når gränsen och börjar sedan att släppa trafik) innebär det att du måste dedikera fler resurser till Lightweight Gateway.|
|Process(Microsoft.Tri.Gateway)\Privata byte|Mängden dedikerat minne (i byte) som Lightweight Gateway-processen faktiskt använder.|Inget tröskelvärde. | Jämför resultatet från den här räknaren med gränsen i maximal storlek för dedikerat minne för GatewayUpdaterResourceManager. Om du ser att processen ofta når gränsen under en tidsperiod (processen når gränsen och börjar sedan att släppa trafik) innebär det att du måste dedikera fler resurser till Lightweight Gateway.| 
|Process(Microsoft.Tri.Gateway)\Arbetsminne|Mängden fysiskt minne (i byte) som Lightweight Gateway-processen faktiskt använder.|Inget tröskelvärde. |Jämför resultatet från den här räknaren med gränsen i storleksgräns för arbetsminne i GatewayUpdaterResourceManager. Om du ser att processen ofta når gränsen under en tidsperiod (processen når gränsen och börjar sedan att släppa trafik) innebär det att du måste dedikera fler resurser till Lightweight Gateway.|

## <a name="ata-center-performance-counters"></a>Prestandaräknare i ATA Center
Du kan se prestandatillståndet i realtid för ATA Center genom att lägga till ATA Centers prestandaräknare.

Detta görs genom att öppna **Prestandaövervakaren** och lägga till alla räknare för ATA Center. Namnet på prestandaräknarobjektet är: **Microsoft ATA Center**.

Här är listan med de viktigaste ATA Center-räknarna som du bör vara medveten om:

> [!div class="mx-tableFixed"]
|Räknare|Beskrivning|Tröskelvärde|Felsökning|
|-----------|---------------|-------------|-------------------|
|Microsoft ATA Center\EntityReceiver – blockstorlek för entitetsbatch|Antal entitetsbatchar som placerats i kö av ATA Center.|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 10 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener.  Referera till det föregående **Process för ATA-komponenter**.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|Microsoft ATA Center\NetworkActivityProcessor – blockstorlek för nätverksaktivitet|Antal nätverksaktiviteter (NA) i kö för bearbetning.|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 50 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Referera till det föregående **Process för ATA-komponenter**.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|Microsoft ATA Center\EntityProfiler – blockstorlek för nätverksaktivitet|Antal nätverksaktiviteter (NA) i kö för profilering.|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 100 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Referera till det föregående **Process för ATA-komponenter**.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|Microsoft ATA Center\Databas &#42; blockstorlek|Antal nätverksaktiviteter av en viss typ i kö för att skrivas till databasen.|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 50 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Referera till det föregående **Process för ATA-komponenter**.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|


> [!NOTE]
> -   Tidsinställda räknare anges i millisekunder
> -   Ibland är det mer praktiskt att övervaka hela listan med räknare med hjälp av diagramtypen för rapport (exempel: realtidsövervakning av alla räknare).

## <a name="operating-system-counters"></a>Operativsystemsräknare
I följande tabell visas de viktigaste räknare för att ta hänsyn till:

> [!div class="mx-tableFixed"]
|Räknare|Beskrivning|Tröskelvärde|Felsökning|
|-----------|---------------|-------------|-------------------|
|Processor(_total)\% Processortid|Procentandelen av förfluten tid som processorn använder för att köra en icke-inaktiv tråd.|Mindre än 80 % i genomsnitt|Kontrollera om det finns en särskild process som tar mycket mer processortid än den borde.<br /><br />Lägg till fler processorer.<br /><br />Minska mängden trafik per server.<br /><br />Räknaren ”Processor(_total)\% Processortid” kan vara mindre exakt på virtuella servrar. Det mer exakta sättet att mäta bristen på processorkraft är då via räknaren ”System\Kölängd för processor”.|
|System\Kontextbyten/s|Den sammanlagda hastigheten som alla processorer byter från en tråd till en annan.|Färre än 5 000&#42;kärnor (fysiska kärnor)|Kontrollera om det finns en särskild process som tar mycket mer processortid än den borde.<br /><br />Lägg till fler processorer.<br /><br />Minska mängden trafik per server.<br /><br />Räknaren ”Processor(_total)\% Processortid” kan vara mindre exakt på virtuella servrar. Det mer exakta sättet att mäta bristen på processorkraft är då via räknaren ”System\Kölängd för processor”.|
|System\Kölängd för processor|Antal trådar som är redo att köra och väntar på att schemaläggas.|Mindre än fem&#42;kärnor (fysiska kärnor)|Kontrollera om det finns en särskild process som tar mycket mer processortid än den borde.<br /><br />Lägg till fler processorer.<br /><br />Minska mängden trafik per server.<br /><br />Räknaren ”Processor(_total)\% Processortid” kan vara mindre exakt på virtuella servrar. Det mer exakta sättet att mäta bristen på processorkraft är då via räknaren ”System\Kölängd för processor”.|
|Minne\Tillgängliga megabyte|Mängden fysiskt minne (RAM) som är tillgängligt för allokering.|Ska vara mer än 512|Kontrollera om det finns en särskild process som tar mycket mer fysiskt minne än den borde.<br /><br />Öka mängden fysiskt minne.<br /><br />Minska mängden trafik per server.|
|Logisk disk(&#42;)\Medel s/diskläsning|Genomsnittlig svarstid för att läsa data från disken (du bör välja databasenheten som instans).|Bör vara mindre än 10 millisekunder|Kontrollera om det finns en särskild process som använder databasenheten mer än den borde.<br /><br />Kontakta din /-leverantören om den här enheten kan leverera den nuvarande arbetsbelastningen med mindre än 10 ms svarstid. Den nuvarande arbetsbelastningen kan fastställas med hjälp av räknarna för diskanvändning.|
|Logisk disk(&#42;)\Medel s/diskskrivning|Genomsnittlig svarstid för att skriva data till disken (du bör välja databasenheten som instans).|Bör vara mindre än 10 millisekunder|Kontrollera om det finns en särskild process som använder databasenheten mer än den borde.<br /><br />Kontakta din eller din lagringsleverantör om den här enheten kan leverera den nuvarande arbetsbelastningen med mindre än 10 ms svarstid. Den nuvarande arbetsbelastningen kan fastställas med hjälp av räknarna för diskanvändning.|
|\Logisk disk(&#42;)\Diskläsningar/s|Frekvensen för att utföra läsåtgärder på disken.|Inget tröskelvärde|Räknarna för diskanvändning kan ge information när du felsöker svarstid för lagring.|
|\Logisk disk(&#42;)\Disk – lästa byte/s|Antal byte per sekund som läses från disken.|Inget tröskelvärde|Räknarna för diskanvändning kan ge information när du felsöker svarstid för lagring.|
|\Logisk disk&#42;\Diskskrivningar/s|Frekvensen för att utföra skrivåtgärder på disken.|Inget tröskelvärde|Räknarna för diskanvändning (kan ge information när du felsöker svarstiden för lagring)|
|\Logisk disk(&#42;)\Disk – skrivna byte/s|Antal byte per sekund som skrivs till disken.|Inget tröskelvärde|Räknarna för diskanvändning kan ge information när du felsöker svarstid för lagring.|

## <a name="see-also"></a>Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-kapacitetsplanering](ata-capacity-planning.md)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Konfigurera vidarebefordran av Windows-händelser](configure-event-collection.md#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
