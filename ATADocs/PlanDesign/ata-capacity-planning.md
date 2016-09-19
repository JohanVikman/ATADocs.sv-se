---
title: Planera din ATA-distribution | Microsoft ATA
description: "Hjälper dig att planera distributionen och bestämma hur många ATA-servrar som krävs för nätverket"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.service: advanced-threat-analytics
ms.prod: 
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: 09bf48be4c651af6ca1ae66a47f940d504570c8a


---

*Gäller för: Advanced Threat Analytics version 1.7*



# ATA-kapacitetsplanering
Det här avsnittet hjälper dig att avgöra hur många ATA-servrar som behövs för att övervaka nätverket, inklusive att förstå hur många ATA-gatewayer och/eller ATA Lightweight-gatewayer du behöver samt serverkapaciteten för ATA Center och ATA Gateway.

##Använda storleksverktyget
Det rekommenderade och enklaste sättet att avgöra kapaciteten för ATA-distributionen är genom att använda [ATA-storleksverktyget](http://aka.ms/atasizingtool). Kör ATA-storleksverktyget och använd följande fält från resultaten i Excel-filen för att avgöra vilken ATA-kapacitet du behöver:

- ATA Center – CPU och minne: Matcha fältet **Upptagna paket/sek** i ATA Center-tabellen i resultatfilen med fältet **PAKET PER SEKUND** i tabellen [ATA Center](#ata-center-sizing).

- ATA Center – Lagring: Matcha fältet **Gmsn paket/sek** i ATA Center-tabellen i resultatfilen med fältet **PAKET PER SEKUND** i tabellen [ATA Center](#ata-center-sizing).
- ATA Gateway: Matcha fältet **Upptagna paket/sek** i tabellen ATA Gateway i resultatfilen med fältet **PAKET PER SEKUND** i [tabellen ATA Gateway](#ata-gateway-sizing) eller [tabellen ATA Lightweight Gateway](#ata-lightweight-gateway-sizing), beroende på vilken [gatewaytyp du väljer](#choosing-the-right-gateway-type-for-your-deployment).


![Exempel på kapacitetsplaneringsverktyg](media/capacity tool.png)



Om du av någon anledning inte kan använda ATA-storleksverktyget måste du manuellt samla in informationen om paket/sek från alla dina domänkontrollanter under 24 timmar med ett mycket lågt insamlingsintervall (ca 5 sekunder). För varje domänkontrollant måste du sedan beräkna dagligt genomsnitt och genomsnitt för den mest hektiska perioden (15 minuter).
I följande avsnitt finns anvisningar om hur du samlar in information om paket/sek från en domänkontrollant.



### Storlek för ATA Center
ATA Center kräver minst 30 dagars data enligt rekommendation för analys av användarbeteende. Nödvändigt diskutrymme för ATA-databasen per domänkontrollant anges nedan. Om du har flera domänkontrollanter beräknar du det fullständiga utrymmet som krävs för ATA-databasen genom att summera nödvändigt diskutrymme per domänkontrollant.
 

|Paket per sekund&#42;|CPU (kärnor&#42;&#42;)|Minne (GB)|Databaslagring per dag (GB)|Databaslagring per månad (GB)|IOPS&#42;&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1,000|2|32|0,3|9|30 (100)
|10,000|4|48|3|90|200 (300)
|40,000|8|64|12|360|500 (1,000)
|100,000|12|96|30|900|1,000 (1,500)
|400 000|40|128|120|1,800|2,000 (2,500)
&#42;Totalt dagligt genomsnittligt antal paket per sekund från alla domänkontrollanter som övervakas av alla ATA-gatewayer.

&#42;&#42;Det omfattar fysiska kärnor, inte hypertrådade kärnor.

&#42;&#42;&#42;Genomsnittligt antal (högsta antal)
> [!NOTE]
> -   ATA Center kan hantera sammanlagt högst 400 000 bilder per sekund (FPS) från alla övervakade domänkontrollanter.
> -   De mängder lagring som anges här är nettovärden. Du bör alltid räkna med framtida tillväxt och se till att disken som databasen ligger på har minst 20 % ledigt utrymme.
> -   Om det lediga utrymmet når minst 20 % eller 100 GB tas den äldsta datasamlingen bort. Detta fortsätter att inträffa fram till det är 5 % eller 50 GB ledigt utrymme kvar då datainsamlingen slutar att fungera.
> -   Lagringssvarstiden för läs- och skrivaktiviteter bör vara under 10 ms.
> -   Förhållandet mellan läs- och skrivaktiviteter är cirka 1:3 under 100 000 paket per sekund och 1:6 över 100 000 paket per sekund.
> -   Vid körning som virtuell dator stöds inte dynamiskt minne och andra funktioner för ballongminne.
> -   För optimala prestanda ställer du in **Energialternativ** för ATA Center på **Höga prestanda**.<br>
> -   När du arbetar på en fysisk server kräver ATA-databasen att du **inaktiverar** NUMA (Non-Uniform Memory Access) i BIOS. NUMA kan kallas Node Interleaving i systemet. I så fall måste du **aktivera** Node Interleaving för att inaktivera NUMA. Mer information finns i BIOS-dokumentationen. Obs! Det här gäller inte när ATA Center körs på en virtuell server.


## Välja rätt gateway-typ för distributionen
I en ATA-distribution stöds valfri kombination av ATA Gateway-typer:

- Endast ATA Gateway
- Endast ATA Lightweight Gateway
- En kombination av båda

Tänk på följande när du bestämmer typ av Gateway-distribution:

|Gateway-typ|Fördelar|Kostnad|Distributionstopologi|Användning av domänkontrollant|
|----|----|----|----|-----|
|ATA Gateway|Out-of-band-distribution gör det svårare för angripare att upptäcka ATA|Högre|Installeras tillsammans med domänkontrollanten (out-of-band)|Har stöd för upp till 50 000 paket per sekund|
|ATA Lightweight Gateway|Kräver inte en dedikerad server och portspeglingskonfiguration|Lägre|Installerad på domänkontrollanten|Har stöd för upp till 10 000 paket per sekund|

Följande är exempel på scenarier där domänkontrollanter bör omfattas av ATA Lightweight Gateway:


- Avdelningskontor

- Virtuella domänkontrollanter som är distribuerade i molnet (IaaS)


Följande är exempel på scenarier där domänkontrollanter bör omfattas av ATA Gateway:


- Datacenter på huvudkontor (med domänkontrollanter med fler än 10 000 paket per sekund)


### Storlek för ATA Lightweight Gateway

En ATA Lightweight Gateway kan stödja övervakning av en domänkontrollant baserat på mängden nätverkstrafik som domänkontrollanten genererar. 


|Paket per sekund&#42;|CPU (kärnor&#42;&#42;)|Minne (GB)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1,000|2|6|
|5 000|6|16|
    |10,000|10|24|

&#42;Totalt antal paket per sekund på domänkontrollanten som övervakas av den specifika ATA Lightweight Gateway.

&#42;&#42;Totalt antal kärnor som inte är flertrådade som den här domänkontrollanten har installerat.<br>Även om flertrådsteknik är godkänd för ATA Lightweight Gateway bör du räkna antalet faktiska kärnor och inte flertrådade kärnor när du planerar kapaciteten.

&#42;&#42;&#42;Total mängd minne som den här domänkontrollanten har installerat.

> [!NOTE]   
> -   Domänkontrollantens prestanda kommer inte att påverkas om den inte har nödvändiga resurser som krävs av ATA Lightweight Gateway, men ATA Lightweight Gateway kanske inte fungerar som förväntat.
> -   Vid körning som virtuell dator stöds inte dynamiskt minne och andra funktioner för ballongminne.
> -   För bästa prestanda ställer du in **Energialternativ** för ATA Lightweight Gateway på **Höga prestanda**.


### Storlek på ATA-gateway

Tänk på följande när du bestämmer hur många ATA-gatewayer som ska distribueras.

-   **Active Directory-skogar och domäner**<br>
    ATA kan övervaka trafik från flera domäner från en enda Active Directory-skog. För att övervaka flera Active Directory-skogar krävs separata ATA-distributioner. En enda ATA-distribution ska inte konfigureras för att övervaka nätverkstrafik från domänkontrollanter från olika skogar.

-   **Portspegling**<br>
Överväganden för portspegling kan kräva att du distribuerar flera ATA-gatewayer per datacenter eller avdelningskontor.

-   **Kapacitet**<br>
    En ATA Gateway har stöd för övervakning av flera domänkontrollanter, beroende på mängden nätverkstrafik för de domänkontrollanter som övervakas. 
<br>



|Paket per sekund&#42;|CPU (kärnor&#42;&#42;)|Minne (GB)|
|---------------------------|-------------------------|---------------|
|1,000|1|6|
|5 000|2|10|
|10,000|3|12|
|20,000|6|24|
|50 000|16|48|
&#42;Totalt genomsnittligt antal paket per sekund från alla domänkontrollanter som övervakas av den specifika ATA-gatewayen under den tid på dagen som är mest aktiv.

&#42;Den totala mängden portspeglad trafik för domänkontrollanter får inte överskrida kapaciteten för avbildningsnätverkskortet på ATA-gatewayen.

&#42;&#42;Hypertrådning måste vara inaktiverad.

> [!NOTE] 
> -   Dynamiskt minne stöds inte.
> -   För bästa prestanda ställer du in **Energialternativ** för ATA Gateway på **Höga prestanda**.


## Beräkning av trafik för domänkontrollanter
Det finns flera olika verktyg du kan använda för identifiering av genomsnittligt antal paket per sekund för domänkontrollanterna. Om du inte har några verktyg som spårar räknaren kan du samla in informationen som krävs med hjälp av Prestandaövervakaren.

Fastställ antal paket per sekund genom att göra följande på varje domänkontrollant:

1.  Öppna Prestandaövervakaren.

    ![Bild av Prestandaövervakaren](media/ATA-traffic-estimation-1.png)

2.  Expandera **Datainsamlaruppsättningar**.

    ![Bild av Datainsamlaruppsättningar](media/ATA-traffic-estimation-2.png)

3.  Högerklicka på **Användardefinierade** och välj **Ny** &gt; **Datainsamlaruppsättning**.

    ![Bild av ny datainsamlaruppsättning](media/ATA-traffic-estimation-3.png)

4.  Ange ett namn på insamlaruppsättningen och välj **Skapa manuellt (avancerat)**.

5.  Under **Vilken typ av data vill du ta med?** väljer du **Skapa dataloggar och Prestandaräknare**.

    ![Bild av typ av data för ny datainsamlaruppsättning](media/ATA-traffic-estimation-5.png)

6.  Under **Vilka prestandaräknare vill du logga?** klickar du på **Lägg till**.

7.  Expandera **Nätverkskort**, välj **Paket per sekund** och välj rätt instans. Om du inte är säker kan du välja **&lt;Alla instanser&gt;** och klicka på **Lägg till** och **OK**.

    > [!NOTE]
    > Om du vill göra det kör du `ipconfig /all` på en kommandorad så att nätverkskortets namn och konfiguration visas.

    ![Bild av hur du lägger till prestandaräknare](media/ATA-traffic-estimation-7.png)

8.  Ändra **Provintervall** till **1 sekund**.

9. Ange den plats där du vill att data ska sparas.

10. Under **Vill du skapa datainsamlaruppsättningen?** väljer du **Starta datainsamlaruppsättningen nu** och klickar på **Slutför**.

    Nu bör du se datainsamlaruppsättningen som du precis har skapat med en grön triangel som anger att den fungerar.

11. Efter 24 timmar stoppar du datainsamlaruppsättningen genom att högerklicka på datainsamlaruppsättningen och välja **Stoppa**.

    ![Bild av hur du stoppar en datainsamlaruppsättning](media/ATA-traffic-estimation-12.png)

12. Bläddra till den mapp där BLG-filen sparades i Utforskaren och dubbelklicka på den så att den öppnas i Prestandaövervakaren.

13. Välj räknaren Paket/s och anteckna genomsnittliga och högsta värden.

    ![Bild av räknaren Paket/s](media/ATA-traffic-estimation-14.png)

## Se även
- [Krav för ATA](ata-prerequisites.md)
- [ATA-arkitektur](ata-architecture.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


