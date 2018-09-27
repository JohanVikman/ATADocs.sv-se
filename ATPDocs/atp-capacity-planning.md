---
title: Planera din Azure Advanced Threat Protection-distribution | Microsoft Docs
description: Hjälper dig att planera distributionen och bestämma hur många Azure ATP-servrar som behövs för nätverket
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: conceptual
ms.service: azure-advanced-threat-protection
ms.prod: ''
ms.assetid: da0ee438-35f8-4097-b3a1-1354ad59eb32
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e894422e7264650186c6f4eea28d5a9099ca7914
ms.sourcegitcommit: 56065ee43dac299203871cd6f025315520750b3b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/26/2018
ms.locfileid: "47233906"
---
*Gäller för: Azure Avancerat skydd*



# <a name="azure-atp-capacity-planning"></a>Azure ATP-kapacitetsplanering
Den här artikeln hjälper dig att avgöra hur många Azure ATP-sensorer och fristående sensorer återställningsprenumeration.

> [!NOTE] 
> Storleksverktyget har två blad – en för ATA och en för Azure ATP. Kontrollera att du är på rätt bladet.

## <a name="using-the-sizing-tool"></a>Använda storleksverktyget
Det rekommendera och enklaste sättet att avgöra kapaciteten för din Azure ATP-distribution är att använda den [Azure ATP-Storleksverktyget](http://aka.ms/aatpsizingtool). Kör Azure ATP-Storleksverktyget och från resultat som Excel-fil, använder du följande fält för att fastställa CPU och minne som används av sensorn:

- Azure ATP-sensorn: matchar den **upptagna paket/sek** i Azure ATP-sensorn tabellen i resultatfilen med den **paket PER sekund** i den [Azure ATP fristående sensorn tabell](#azure-atp-sensor-sizing)eller [Azure ATP-sensorn tabell](#azure-atp-standalone-sensor-sizing), beroende på den [sensor databastyp du väljer](#choosing-the-right-sensor-type-for-your-deployment).


![Exempel på kapacitetsplaneringsverktyg](media/capacity-tool.png)


Om du inte kan använda Azure ATP-Storleksverktyget av någon anledning, manuellt samla in informationen om paket/sek från alla dina domänkontrollanter under 24 timmar med ett lågt insamlingsintervall (ca 5 sekunder). För varje domänkontrollant måste du sedan beräkna dagligt genomsnitt och genomsnitt för den mest hektiska perioden (15 minuter).
I följande avsnitt finns anvisningar om hur du samlar in information om paket/sek från en domänkontrollant.

## Välja rätt sensor-typ för din distribution<a name="choosing-the-right-sensor-type-for-your-deployment"></a>
I en Azure ATP-distribution stöds valfri kombination av Azure ATP fristående sensorn typer:

- Endast Azure ATP fristående sensorer
- Azure ATP-sensorn
- En kombination av båda

När du bestämmer typ av sensor-distribution, Överväg följande fördelar:

|typ av sensor|Fördelar|Kostnad|Distributionstopologi|Användning av domänkontrollant|
|----|----|----|----|-----|
|Azure ATP fristående sensor|Out of band-distribution gör det svårare för angripare att upptäcka Azure ATP finns|Högre|Installeras tillsammans med domänkontrollanten (out-of-band)|Har stöd för upp till 100 000 paket per sekund|
|Azure ATP-sensorn|Kräver inte en dedikerad server och portspeglingskonfiguration|Lägre|Installerad på domänkontrollanten|Har stöd för upp till 100 000 paket per sekund|

Tänk på följande när du bestämmer hur många Azure ATP fristående sensorer för att distribuera.

-   **Active Directory-skogar och domäner**<br>
    Azure ATP kan övervaka trafik från flera domäner i flera Active Directory-skogar för varje arbetsyta som du skapar. 

-   **Portspegling**<br>
Överväganden för portspegling kan kräva att du kan distribuera flera fristående Azure ATP-sensorer per plats för data Datacenter eller avdelningskontor.

-   **Kapacitet**<br>
    En fristående Azure ATP-sensorn har stöd för övervakning av flera domänkontrollanter, beroende på mängden nätverkstrafik för de domänkontrollanter som övervakas. 


## Azure ATP-sensorn och fristående sensorn storlek <a name="sizing"></a>

Azure ATP-sensorn har stöd för övervakning av en domänkontrollant baserat på mängden nätverkstrafik som domänkontrollanten genererar. I följande tabell är en uppskattning, den slutliga mängd som sensorn Parsar beror på mängden trafik och distribuering av trafik. 
> [!NOTE]
> Följande kapacitet för CPU och minne refererar till sensorns egen förbrukning – inte domänkontrollantens kapacitet.

|Paket per sekund *|CPU (kärnor)|Minne (GB)|
|----|----|-----|
|0 – 1 k|0.25|2,50|
|1k - 5k|0,75|6.00|
|5k - 10k|1,00|6.50|
|10k - 20k|2,00|9.00|
|20k - 50k|3.50|9,50|
|50k - 75k |3.50|9,50|
|75k - 100 kB|3.50 |9,50|

> [!NOTE]
> - Totalt antal kärnor som ska användas av sensortjänsten.<br>Vi rekommenderar att du inte arbetar med hypertrådade kärnor.
> - Total mängd minne som ska användas av sensortjänsten.
> -   Om domänkontrollanten inte har de resurser som krävs av Azure ATP-sensorn domänkontrollantens prestanda påverkas inte, men Azure ATP-sensorn kanske inte fungerar som förväntat.
> -   Vid körning som virtuell dator stöds inte dynamiskt minne och andra funktioner för ballongminne.
> -   För optimala prestanda ställer du in den **Energialternativ** för Azure ATP-sensorn till **högpresterande**.
> -   Minst 2 kärnor och 6 GB utrymme krävs och 10 GB rekommenderas, inklusive utrymme som krävs för Azure ATP-binärfiler och loggar.


## <a name="domain-controller-traffic-estimation"></a>Beräkning av trafik för domänkontrollanter

Det finns flera olika verktyg du kan använda för identifiering av genomsnittligt antal paket per sekund för domänkontrollanterna. Om du inte har några verktyg som spårar räknaren kan du samla in informationen som krävs med hjälp av Prestandaövervakaren.

Fastställ antal paket per sekund genom att utföra följande steg på varje domänkontrollant:

1.  Öppna Prestandaövervakaren.

    ![Bild av Prestandaövervakaren](media/atp-traffic-estimation-1.png)

2.  Expandera **Datainsamlaruppsättningar**.

    ![Bild av Datainsamlaruppsättningar](media/atp-traffic-estimation-2.png)

3.  Högerklicka på **Användardefinierade** och välj **Ny** &gt; **Datainsamlaruppsättning**.

    ![Bild av ny datainsamlaruppsättning](media/atp-traffic-estimation-3.png)

4.  Ange ett namn på insamlaruppsättningen och välj **Skapa manuellt (avancerat)**.

5.  Under **Vilken typ av data vill du ta med?** väljer du **Skapa dataloggar och Prestandaräknare**.

    ![Bild av typ av data för ny datainsamlaruppsättning](media/atp-traffic-estimation-5.png)

6.  Under **Vilka prestandaräknare vill du logga?** klickar du på **Lägg till**.

7.  Expandera **Nätverkskort**, välj **Paket per sekund** och välj rätt instans. Om du inte är säker kan du välja **&lt;Alla instanser&gt;** och klicka på **Lägg till** och **OK**.

    > [!NOTE]
    > Om du vill utföra den här åtgärden på en kommandorad kör du `ipconfig /all` för att visa namnet på nätverkskortet och konfigurationen.

    ![Bild av hur du lägger till prestandaräknare](media/atp-traffic-estimation-7.png)

8.  Ändra den **provintervall** till **fem sekunder**.

9. Ange den plats där du vill att data ska sparas.

10. Under **skapa datainsamlaruppsättningen**väljer **starta datainsamlaruppsättningen nu**, och klicka på **Slutför**.

    Nu bör du se datainsamlaruppsättningen som du skapade med en grön triangel som anger att den fungerar.

11. Efter 24 timmar stoppar du datainsamlaruppsättningen genom att högerklicka på datainsamlaruppsättningen och välja **Stoppa**.

    ![Bild av hur du stoppar en datainsamlaruppsättning](media/atp-traffic-estimation-12.png)

12. Bläddra till den mapp där BLG-filen sparades i Utforskaren och dubbelklicka på den så att den öppnas i Prestandaövervakaren.

13. Välj räknaren Paket/s och anteckna genomsnittliga och högsta värden.

    ![Bild av räknaren Paket/s](media/atp-traffic-estimation-14.png)



## <a name="see-also"></a>Se även
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Azure ATP-arkitektur](atp-architecture.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
