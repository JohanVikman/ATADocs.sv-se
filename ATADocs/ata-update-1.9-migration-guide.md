---
title: Advanced Threat Analytics-uppdatering till 1,9 Migreringsguide | Microsoft Docs
description: Procedurer för att uppdatera ATA till version 1.9
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 03/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: bd96cf2b2048aa37e559649d15565c3244684e35
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166007"
---
# <a name="updating-ata-to-version-19"></a>Uppdatera ATA till version 1.9

> [!NOTE] 
> Om ATA inte är installerat i miljön kan du hämta den fullständiga versionen av ATA, som innehåller version 1.9 och följa standardproceduren för installation som beskrivs i [installera ATA](install-ata-step1.md).

Om du redan har ATA version 1.8 distribuerat vägleder den här proceduren dig genom steg som krävs för att uppdatera distributionen.

> [!NOTE] 
>  Endast ATA version 1.8 (1.8.6645) och ATA 1.8 uppdatering 1 (1.8.6765) kan uppdateras till ATA version 1.9, en tidigare version av ATA kan inte uppdateras direkt till ATA version 1.9.

Följ dessa steg för att uppdatera till ATA version 1.9:

1.  [Ladda ned uppdateringsversionen av ATA 1.9 från Download Center](https://www.microsoft.com/download/details.aspx?id=56725) eller den fullständiga versionen från den [Evaluation center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
I migreringsversionen kan kan filen användas för att endast uppdatera från ATA 1.8. I versionen från Evaluation Center används samma installationsfil (Microsoft ATA Center Setup.exe) för att installera en ny distribution av ATA och för att uppgradera befintliga distributioner.

2.  Uppdatera ATA Center

4.  Uppdatera ATA Gateways

    > [!IMPORTANT]
    > Uppdatera alla ATA Gateways för att säkerställa att ATA fungerar korrekt.

### <a name="step-1-update-the-ata-center"></a>Steg 1: Uppdatera ATA Center

1.  Säkerhetskopiera databasen: (valfritt)

    -   Om ATA Center körs som en virtuell dator och du vill ha en kontrollpunkt, stänga av den virtuella datorn först.

    -   Om ATA Center körs på en fysisk server läser du artikeln om [haveriberedskap](disaster-recovery.md) för information om hur du säkerhetskopierar databasen.

2.  Kör installationsfilen, **Microsoft ATA Center Setup.exe**, och följ anvisningarna på skärmen för att installera uppdateringen.

    -  På sidan **Välkommen** väljer du språk och klickar på **Nästa**.

    -  Om du inte aktiverar automatiska uppdateringar i version 1.8, uppmanas du att konfigurera ATA att använda Microsoft Update för att ATA ska hållas uppdaterad.  På sidan Microsoft Update markerar du **Använd Microsoft Update när jag söker efter uppdateringar (rekommenderas)**.
    ![Håll ATA uppdaterat bild](media/ata_ms_update.png)
     
     Detta justerar Windows-inställningarna för att aktivera uppdateringar för ATA. 
    
    -  Den **partiella datamigrering** skärmen får du reda på att tidigare avbildade nätverkstrafik, händelser, entiteter och identifiering av relaterade data tas bort. Alla identifieringar arbeta direkt med undantag för identifieringen för onormalt beteende onormal grupp ändringar, rekognosering med katalogtjänster (SAM-R) och kryptering nedgradering identifieringar vilket ta upp till tre veckor för att skapa en fullständig profil efter den obligatoriska samtidigt. 
     
      ![ATA partiell migrering](media/partial-migration.png)

    -  Klicka på **Uppdatera**. När du har klickat på Uppdatera är ATA offline tills uppdateringsproceduren har slutförts.

4.  När ATA Center-uppdateringen är klar klickar du på **Starta** för att öppna skärmen **Uppdatera** i ATA-konsolen för ATA-gatewayar.

     ![Skärm för uppdateringen lyckades](media/migration-center-success.png)

5.  I den **uppdateringar** skärm, om du redan har ATA-gatewayer för att automatiskt uppdatera de uppdateras nu, om inte, klickar du på **uppdatera** bredvid varje ATA Gateway.
  
     ![Bild av uppdatera gatewayar](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Uppdatera alla ATA Gateways för att säkerställa att ATA fungerar korrekt.
 
> [!NOTE] 
> Om du vill installera nya ATA-gatewayer går den **gatewayer** skärmen och klicka på **hämta installationsprogram för Gateway** att hämta ATA 1.9 Gateway-installationspaketet och följ anvisningarna för nya Gateway-installationen som Mer information finns i [steg 4. Installera ATA Gateway](install-ata-step4.md).


## <a name="see-also"></a>Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
