---
title: "Migreringsguide för ATA-uppdatering till 1.7 | Microsoft ATA"
description: "Procedurer för att uppdatera ATA till version 1.7"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: 5c20c41c3fe587f18087d64f4f84c1df65072fde


---

# Migreringsguide för ATA-uppdatering till 1.7
Uppdateringen för ATA 1.7 ger förbättringar inom följande områden:

-   Nya identifieringar

-   Förbättringar av befintliga identifieringar
  

## Uppdatera ATA till version 1.7
> [!NOTE] 
> Om ATA inte är installerat i miljön kan du hämta den fullständiga versionen av ATA, som innehåller version 1.7, och följa standardproceduren för installation som beskrivs i [Installera ATA](/advanced-threat-analytics/deploy-use/install-ata).

Om du redan har distribuerat ATA version 1.6 vägleder den här proceduren dig igenom de steg som krävs för att uppdatera distributionen.

> [!NOTE] 
> Du kan inte installera ATA version 1.7 direkt på ATA version 1.4 eller 1.5. Du måste först installera ATA version 1.6. 

Följ dessa steg för att uppdatera till ATA version 1.7:

1.  [Hämta uppdateringen 1.7](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
I den här versionen används samma installationsfil (Microsoft ATA Center Setup.exe) för att installera en ny distribution av ATA och för att uppgradera befintliga distributioner.

2.  Uppdatera ATA Center

4.  Uppdatera ATA Gateways

    > [!IMPORTANT]
    > Uppdatera alla ATA Gateways för att säkerställa att ATA fungerar korrekt.

### Steg 1: Uppdatera ATA Center

1.  Säkerhetskopiera databasen: (valfritt)

    -   Om ATA Center körs som en virtuell dator och du vill göra en kontrollpunkt ska du först stänga av den virtuella datorn.

    -   Om ATA Center körs på en fysisk server ska du följa den rekommenderade proceduren för att [säkerhetskopiera MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Kör installationsfilen, **Microsoft ATA Center Setup.exe**, och följ anvisningarna på skärmen för att installera uppdateringen.

    -  På sidan **Välkommen** väljer du språk och klickar på **Nästa**.

    -  Om du inte aktiverat automatiska uppdateringar i version 1.6, uppmanas du att ställa in ATA till att använda Microsoft Update för att ATA ska hållas uppdaterad.  På sidan Microsoft Update markerar du **Använd Microsoft Update när jag söker efter uppdateringar (rekommenderas)**.
    ![Bild för att hålla ATA uppdaterat](media/ata_ms_update.png) Detta justerar Windows-inställningarna för att aktivera uppdateringar för andra Microsoft-produkter (inklusive ATA), på det sätt som visas här. 
     ![Bild för automatisk uppdatering av Windows](media/ata_installupdatesautomatically.png)

    -  På skärmen **Datamigrering** väljer du om du vill migrera alla eller partiella data. Om du väljer att migrera endast partiella data migreras inte din tidigare avbildade nätverkstrafik och beteendeprofiler kommer inte att migreras. Detta innebär att det tar tre veckor innan identifieringen av onormalt beteende har en klar profil för att aktivera identifiering av onormal aktivitet. Under dessa tre veckor kommer alla andra ATA-identifieringar att fungera korrekt. Migrering av **partiella** data tar mycket kortare tid att installera. Om du väljer **fullständig** datamigrering, kan det ta väldigt lång tid att slutföra installationen. Den uppskattade mängden tid och det nödvändiga diskutrymmet, som visas på skärmen **Datamigrering**, beror på mängden tidigare avbildad nätverkstrafik som du sparat i tidigare versioner av ATA. Innan du väljer **partiell** eller **fullständig**, se till att kontrollera kraven.  
    
    ![ATA-datamigrering](media/migration data migration.png)

    -  Klicka på **Uppdatera**. När du har klickat på Uppdatera är ATA offline tills uppdateringsproceduren har slutförts.

4.  När ATA Center-uppdateringen är klar klickar du på **Starta** för att öppna skärmen **Uppdatera** i ATA-konsolen för ATA-gatewayar.
    ![Skärm för uppdateringen lyckades](media/migration center success.png)

5.  På skärmen **Uppdateringar**, om du har angett att ATA-gatewayer automatiskt ska uppdateras, kommer de att uppdateras nu, om inte, klicka på **Uppdatera** bredvid varje ATA Gateway.
  ![Bild av uppdatera gatewayar](media/migration update gw.png)

  
> [!IMPORTANT] 
> Uppdatera alla ATA Gateways för att säkerställa att ATA fungerar korrekt.
> Den konfigurerade Syslog-lyssnarporten på alla gatewayar ändras till 514.
 
    > [!NOTE] 
    > To install new ATA Gateways, go the **Gateways** screen and click **Download Gateway Setup** to get the ATA 1.7 installation package and follow the instructions for new Gateway installation as described in [Step 4. Install the ATA Gateway](/advanced-threat-analytics/deploy-use/install-ata-step4) .



## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->

