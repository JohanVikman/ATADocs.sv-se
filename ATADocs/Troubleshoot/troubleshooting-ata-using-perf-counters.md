---
title: "Felsöka ATA med prestandaräknarna | Microsoft Advanced Threat Analytics"
description: "Beskriver hur du kan använda prestandaräknare för att felsöka problem med ATA"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: df162a62-f273-4465-9887-94271f5000d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 21d87591c9c791aa431c273479921e1c11825e09


---

# Felsöka ATA med prestandaräknarna
ATA-prestandaräknarna ger information om hur bra varje komponent i ATA fungerar. Komponenterna i ATA bearbetar data i tur och ordning. Om ett problem uppstår kan det därför leda till förlorad trafik någonstans i komponentkedjan. För att åtgärda problemet måste du ta reda på vilken komponent som krånglar och åtgärda problemet i början av kedjan. Använd data i prestandaräknarna för att förstå hur varje komponent fungerar.
Mer information om flödet av interna ATA-komponenter finns i [ATA-arkitektur](/advanced-threat-analytics/plan-design/ata-architecture).

**Process för ATA-komponenter**:

1.  När en komponent når maximal storlek blockerar den föregående komponent från att skicka fler entiteter till den.

2.  Slutligen börjar föregående komponent öka **sin** egen storlek tills den blockerar komponenten före den från att skicka fler entiteter.

3.  Det inträffar ända tillbaka till den första NetworkListener-komponenten, som förlorar trafik när den inte längre kan vidarebefordra entiteter.


## Prestandaräknare i ATA Gateway

I det här avsnittet avser varje hänvisning till ATA Gateway också ATA Lightweight Gateway.

Du kan se prestandatillståndet i realtid för ATA-gatewayen genom att lägga till ATA-gatewayens prestandaräknare.
Det gör du genom att öppna Prestandaövervakaren och lägga till alla räknare för ATA-gatewayen. Namnet på prestandaräknarobjektet är: "Microsoft ATA Gateway".

![Bild av hur du lägger till prestandaräknare](media/ATA-performance-counters.png)

Här är listan med de viktigaste ATA Gateway-räknarna som du bör vara medveten om:

|Räknare|Beskrivning|Tröskelvärde|Felsökning|
|-----------|---------------|-------------|-------------------|
|NetworkListener PEF parsermeddelanden/sek|Mängden trafik som bearbetas av ATA Gateway varje sekund.|Inget tröskelvärde|Hjälper dig att förstå mängden trafik som parsas av ATA Gateway.|
|NetworkListener PEF förlorade händelser/sek|Mängden trafik som förloras av ATA Gateway varje sekund.|Det här antalet bör alltid vara noll (sällsynta korta förekomster av förlorade meddelanden är godtagbara).|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|NetworkListener ETW förlorade händelser/sek|Mängden trafik som förloras av ATA Gateway varje sekund.|Det här antalet bör alltid vara noll (sällsynta korta förekomster av förlorade meddelanden är godtagbara).|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|NetworkActivityTranslator – blockstorlek för meddelandedatanummer|Mängden trafik i kö för översättning till nätverksaktiviteter (NA).|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 100 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|EntityResolver – blockstorlek för aktivitet|Antal nätverksaktiviteter (NA) i kö för matchning.|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 10 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|EntitySender – blockstorlek för entitetsbatch|Antal nätverksaktiviteter (NA) i kö för att skickas till ATA Center.|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 1 000 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|EntitySender – sändningstid för batch|Tiden det tog att skicka den senaste batchen.|Bör oftast vara mindre än 1 000 millisekunder|Kontrollera om det finns några nätverksproblem mellan ATA Gateway och ATA Center.|

> [!NOTE]
> -   Tidsinställda räknare anges i millisekunder.
> -   Ibland är det mer praktiskt att övervaka hela listan med räknare med hjälp av diagramtypen Rapport (exempel: realtidsövervakning av alla räknare)

## Prestandaräknare i ATA Center
Du kan se prestandatillståndet i realtid för ATA Center genom att lägga till ATA Centers prestandaräknare.

Det gör du genom att öppna Prestandaövervakaren och lägga till alla räknare för ATA Center. Namnet på prestandaräknarobjektet är: "Microsoft ATA Center".

![Lägga till prestandaräknare i ATA Center](media/ATA-Gateway-perf-counters.png)

Här är listan med de viktigaste ATA Center-räknarna som du bör vara medveten om:

|Räknare|Beskrivning|Tröskelvärde|Felsökning|
|-----------|---------------|-------------|-------------------|
|EntityReceiver – blockstorlek för entitetsbatch|Antal entitetsbatchar som placerats i kö av ATA Center.|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 10 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener.  Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|NetworkActivityProcessor – blockstorlek för nätverksaktivitet|Antal nätverksaktiviteter (NA) i kö för bearbetning.|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 50 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|EntityProfiler – blockstorlek för nätverksaktivitet|Antal nätverksaktiviteter (NA) i kö för profilering.|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 10 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|
|CenterDatabase & #42; Blockstorlek|Antal nätverksaktiviteter av en viss typ i kö för att skrivas till databasen.|Bör vara mindre än maxvärdet-1 (standardmaxvärde: 50 000)|Kontrollera om det finns någon komponent som nått maximal storlek och blockerar tidigare komponenter ända till NetworkListener. Se **Process för ATA-komponenter** ovan.<br /><br />Kontrollera att det inte finns något problem med CPU eller minne.|


> [!NOTE]
> -   Tidsinställda räknare anges i millisekunder
> -   Ibland är det mer praktiskt att övervaka hela listan med räknare med hjälp av diagramtypen för Rapport (exempel: realtidsövervakning av alla räknare).

## Operativsystemsräknare
Följande är listan med de viktigaste operativsystemsräknarna som du bör vara medveten om:

|Räknare|Beskrivning|Tröskelvärde|Felsökning|
|-----------|---------------|-------------|-------------------|
|Processor(_total)\% Processortid|Procentandelen av förfluten tid som processorn använder för att köra en icke-inaktiv tråd.|Mindre än 80 % i genomsnitt|Kontrollera om det finns en särskild process som tar mycket mer processortid än den borde.<br /><br />Lägg till fler processorer.<br /><br />Minska mängden trafik per server.<br /><br />Räknaren ”Processor(_total)\% Processortid” kan vara mindre exakt på virtuella servrar. Det mer exakta sättet att mäta bristen på processorkraft är då via räknaren ”System\Kölängd för processor”.|
|System\Kontextbyten/s|Den sammanlagda hastigheten som alla processorer byter från en tråd till en annan.|Färre än 5 000&#42;kärnor (fysiska kärnor)|Kontrollera om det finns en särskild process som tar mycket mer processortid än den borde.<br /><br />Lägg till fler processorer.<br /><br />Minska mängden trafik per server.<br /><br />Räknaren ”Processor(_total)\% Processortid” kan vara mindre exakt på virtuella servrar. Det mer exakta sättet att mäta bristen på processorkraft är då via räknaren ”System\Kölängd för processor”.|
|System\Kölängd för processor|Antal trådar som är redo att köra och väntar på att schemaläggas.|Färre än 5&#42;kärnor (fysiska kärnor)|Kontrollera om det finns en särskild process som tar mycket mer processortid än den borde.<br /><br />Lägg till fler processorer.<br /><br />Minska mängden trafik per server.<br /><br />Räknaren ”Processor(_total)\% Processortid” kan vara mindre exakt på virtuella servrar. Det mer exakta sättet att mäta bristen på processorkraft är då via räknaren ”System\Kölängd för processor”.|
|Minne\Tillgängliga megabyte|Mängden fysiskt minne (RAM) som är tillgängligt för allokering.|Bör vara mer än 512|Kontrollera om det finns en särskild process som tar mycket mer fysiskt minne än den borde.<br /><br />Öka mängden fysiskt minne.<br /><br />Minska mängden trafik per server.|
|Logisk disk(&#42;)\Medel Disk s/läsning|Genomsnittlig svarstid för att läsa data från disken (du bör välja databasenheten som instans).|Bör vara mindre än 10 millisekunder|Kontrollera om det finns en särskild process som använder databasenheten mer än den borde.<br /><br />Kontrollera med lagringsteamet/-leverantören om den här enheten kan leverera den nuvarande arbetsbelastningen med en svarstid på mindre än 10 ms. Den nuvarande arbetsbelastningen kan fastställas med hjälp av räknarna för diskanvändning.|
|Logisk disk(&#42;)\Medel Disk s/skrivning|Genomsnittlig svarstid för att skriva data till disken (du bör välja databasenheten som instans).|Bör vara mindre än 10 millisekunder|Kontrollera om det finns en särskild process som använder databasenheten mer än den borde.<br /><br />Kontrollera med lagringsteamet/-leverantören om den här enheten kan leverera den nuvarande arbetsbelastningen med en svarstid på mindre än 10 ms. Den nuvarande arbetsbelastningen kan fastställas med hjälp av räknarna för diskanvändning.|
|\Logisk disk(&#42;)\Diskläsningar/s|Frekvensen för att utföra läsåtgärder på disken.|Inget tröskelvärde|Räknarna för diskanvändning kan ge information när du felsöker svarstid för lagring.|
|\Logisk disk(&#42;)\Disk - lästa byte/s|Antal byte per sekund som läses från disken.|Inget tröskelvärde|Räknarna för diskanvändning kan ge information när du felsöker svarstid för lagring.|
|\Logisk disk&#42;\Diskskrivningar/s|Frekvensen för att utföra skrivåtgärder på disken.|Inget tröskelvärde|Räknarna för diskanvändning (kan ge information när du felsöker svarstiden för lagring)|
|\Logisk disk(&#42;)\Disk - skrivna byte/s|Antal byte per sekund som skrivs till disken.|Inget tröskelvärde|Räknarna för diskanvändning kan ge information när du felsöker svarstid för lagring.|

## Se även
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA-kapacitetsplanering](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [Konfigurera händelseinsamling](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [Konfigurera vidarebefordran av Windows-händelser](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


