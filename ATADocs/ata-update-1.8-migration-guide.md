---
title: "Migreringsguide för Advanced Threat Analytics-uppdatering till 1.8 | Microsoft Docs"
description: "Procedurer för att uppdatera ATA till version 1.8"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/9/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e5a9718c-b22e-41f7-a614-f00fc4997682
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: ff61d12eefaf6fb0a6b3d92568ef8c25c9d4c49b
ms.sourcegitcommit: 3177d5894413fbd363b9aca8130f3f7a369223b8
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 07/10/2017
---
# Uppdatera ATA till version 1.8
<a id="updating-ata-to-version-18" class="xliff"></a>

> [!NOTE] 
> Om ATA inte är installerat i miljön kan du hämta den fullständiga versionen av ATA, som innehåller version 1.8, och följa standardproceduren för installation som beskrivs i [Installera ATA](install-ata-step1.md).

Om du redan har distribuerat ATA version 1.7 vägleder den här proceduren dig igenom de steg som krävs för att uppdatera distributionen.

> [!NOTE] 
>  Endast ATA version 1.7 Update 1 och 1.7 Update 2 kan uppdateras till ATA version 1.8. Tidigare versioner av ATA kan inte uppdateras direkt till ATA version 1.8.

Följ dessa steg för att uppdatera till ATA version 1.8:

1.  [Ladda ned uppdateringsversionen av ATA 1.8 från Download Center](https://www.microsoft.com/download/details.aspx?id=55536)  eller den fullständiga versionen från [Evaluation Center](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics).<br>
I migreringsversionen kan filen bara användas för uppdatering från ATA 1.7. I versionen från Evaluation Center används samma installationsfil (Microsoft ATA Center Setup.exe) för att installera en ny distribution av ATA och för att uppgradera befintliga distributioner.

2.  Uppdatera ATA Center

4.  Uppdatera ATA Gateways

    > [!IMPORTANT]
    > Uppdatera alla ATA Gateways för att säkerställa att ATA fungerar korrekt.

### Steg 1: Uppdatera ATA Center
<a id="step-1-update-the-ata-center" class="xliff"></a>

1.  Säkerhetskopiera databasen: (valfritt)

    -   Om ATA Center körs som en virtuell dator och du vill göra en kontrollpunkt ska du först stänga av den virtuella datorn.

    -   Om ATA Center körs på en fysisk server läser du artikeln om [haveriberedskap](disaster-recovery.md) för information om hur du säkerhetskopierar databasen.

2.  Kör installationsfilen, **Microsoft ATA Center Setup.exe**, och följ anvisningarna på skärmen för att installera uppdateringen.

    -  På sidan **Välkommen** väljer du språk och klickar på **Nästa**.

    -  Om du inte aktiverade automatiska uppdateringar i version 1.7 uppmanas du att konfigurera ATA att använda Microsoft Update så att tjänsten hålls uppdaterad.  På sidan Microsoft Update markerar du **Använd Microsoft Update när jag söker efter uppdateringar (rekommenderas)**.
    ![Bild om att håll ATA uppdaterat](media/ata_ms_update.png)
     
     Detta justerar Windows-inställningar så att uppdateringar för ATA aktiveras. 
    
    -  På skärmen **Datamigrering** väljer du om du vill migrera alla eller partiella data. Om du väljer att endast migrera partiella data fungerar alla identifieringar omedelbart med undantag för identifieringen för onormalt beteende, som behöver tre veckor för att skapa en fullständig profil.  
    
    Migrering av **partiella** data går mycket snabbare att installera. Om du väljer **fullständig** datamigrering, kan det ta väldigt lång tid att slutföra installationen. Notera den uppskattade tiden och det nödvändiga diskutrymmet som visas på skärmen **Datamigrering**. Dessa siffror beror på mängden tidigare insamlad nätverkstrafik som du har sparat i tidigare versioner av ATA. Skärmen nedan visar ett exempel på en datamigrering från en mycket stor databas:
         
    ![ATA-datamigrering](media/migration-data-migration.png)

    -  Klicka på **Uppdatera**. När du har klickat på Uppdatera är ATA offline tills uppdateringsproceduren har slutförts.

4.  När ATA Center-uppdateringen är klar klickar du på **Starta** för att öppna skärmen **Uppdatera** i ATA-konsolen för ATA-gatewayar.

    ![Skärm för uppdateringen lyckades](media/migration-center-success.png)

5.  På skärmen **Uppdateringar**, om du har angett att ATA-gatewayer automatiskt ska uppdateras, kommer de att uppdateras nu, om inte, klicka på **Uppdatera** bredvid varje ATA Gateway.
  
![Bild av uppdatera gatewayar](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> Uppdatera alla ATA Gateways för att säkerställa att ATA fungerar korrekt.
 
> [!NOTE] 
> Om du vill installera nya ATA-gatewayer går du till skärmen **Gatewayer** och klickar på **Download Gateway Setup** (Hämta konfiguration för gateway) för att ladda ned ATA Gateway 1.8 -installationspaketet och följer sedan anvisningarna för den nya gatewayinstallationen, som beskrivs i [Steg 4. Installera ATA Gateway](install-ata-step4.md).


## Se även
<a id="see-also" class="xliff"></a>

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)