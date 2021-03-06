---
title: Migreringsguide för Advanced Threat Analytics-uppdatering till 1.6 | Microsoft Docs
description: Procedurer för att uppdatera ATA till version 1.6
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 0756ef64-3aef-4a69-8981-24fa8f285c6a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b32e8db898df1cea25e3d8dbb61a7c2293128aeb
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/18/2018
ms.locfileid: "46134018"
---
# <a name="ata-update-to-16-migration-guide"></a>Migreringsguide för ATA-uppdatering till 1.6
Uppdateringen för ATA 1.6 ger förbättringar inom följande områden:

-   Nya identifieringar

-   Förbättringar av befintliga identifieringar

-   ATA Lightweight Gateway

-   Automatiska uppdateringar

-   Förbättrad prestanda för ATA Center

-   Lägre lagringskrav

-   Stöd för IBM QRadar

## <a name="updating-ata-to-version-16"></a>Uppdatera ATA till version 1.6
> [!NOTE] 
> Om ATA inte är installerat i miljön kan du hämta den fullständiga versionen av ATA, som innehåller version 1.6, och följa standardproceduren för installation som beskrivs i [installera ATA](install-ata-step1.md).

Om du redan har distribuerat ATA version 1.5 vägleder dig genom steg som krävs för att uppdatera distributionen i den här proceduren.

> [!NOTE] 
> Du kan inte installera ATA version 1.6 direkt på ATA version 1.4. Du måste först installera ATA version 1.5. Om du av misstag har försökt installera ATA 1.6 utan att installera ATA 1.5, du får ett felmeddelande som säger att **en nyare version är redan installerad på datorn.** Du måste avinstallera resterna av ATA 1.6 som finns kvar på datorn – trots att installationen misslyckades, innan du installerar ATA version 1.5.

Följ dessa steg för att uppdatera till ATA version 1.6:

1. Undvik uppgraderingsproblem genom att följa steg 8 till 10 i **Migreringsfel vid uppdatering till ATA version 1.6** som beskrivs i [Nyheter i ATA version 1.6](whats-new-version-1.6.md).
2. Kontrollera att du har det lediga utrymme som krävs för att slutföra uppgraderingen. Du kan utföra installationen fram till beredskapskontrollen för att få en beräkning av hur mycket ledigt utrymme som krävs, och sedan starta om uppgraderingen efter att det nödvändiga diskutrymmet har tilldelats.
1.  [Hämta uppdateringen 1.6](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
I den här versionen används samma installationsfil (Microsoft ATA Center Setup.exe) för att installera en ny distribution av ATA och för att uppgradera befintliga distributioner.

2.  Uppdatera ATA Center

3.  Hämta det uppdaterade Gateway-paketet för ATA

4.  Uppdatera ATA Gateways

    > [!IMPORTANT]
    > Uppdatera alla ATA Gateways för att säkerställa att ATA fungerar korrekt.

### <a name="step-1-update-the-ata-center"></a>Steg 1: Uppdatera ATA Center

1.  Säkerhetskopiera databasen: (valfritt)

    -   Om ATA Center körs som en virtuell dator och du vill ha en kontrollpunkt, stänga av den virtuella datorn först.

    -   Om ATA Center körs på en fysisk server ska du följa den rekommenderade proceduren för att [säkerhetskopiera MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Kör installationsfilen, Microsoft ATA Center Setup.exe, och följ anvisningarna på skärmen för att installera uppdateringen.

    1.  ATA 1.6 kräver att .Net Framework 4.6.1 är installerat. Om du inte redan är installerat ATA-installationen installeras .net Framework 4.6.1 som en del av installationen.
    
        > [!NOTE] 
        > Installationen av .Net Framework 4.6.1 kan kräva att servern startas om. ATA-installationen fortsätter först efter att servern har startats om.
    
    2.  På sidan **Välkommen** väljer du språk och klickar på **Nästa**.

    3.  Läs licensavtalet och om du godkänner licensvillkoren klickar du på **nästa**.

    4.  Det är nu möjligt att använda Microsoft Update för att hålla ATA uppdaterat.  På sidan Microsoft Update markerar du **Använd Microsoft Update när jag söker efter uppdateringar (rekommenderas)**.
    ![Håll ATA uppdaterat bild](media/ata_ms_update.png) detta justerar Windows-inställningar för att aktivera uppdateringar för andra Microsoft-produkter (inklusive ATA), som visas här. 
     ![Bild om automatisk uppdatering av Windows](media/ata_installupdatesautomatically.png)

    5.  Innan installationen påbörjas utför ATA en beredskapskontroll. Granska resultatet av kontrollen för att se till att kraven har konfigurerats och att du har minst den minsta mängden ledigt diskutrymme. 
    ![Bild om ATA-beredskapskontroll](media/ata_install_readinesschecks.png)

    6.  Klicka på **Uppdatera**. När du har klickat på Uppdatera är ATA offline tills uppdateringsproceduren har slutförts.

3.  När du har uppdaterat ATA Center rapporterar ATA Gateways att de nu är föråldrade.

    ![Bild av föråldrade gateways](media/ATA-center-outdated.png)

> [!IMPORTANT] 
> Uppdatera alla ATA Gateways för att säkerställa att ATA fungerar korrekt.

### <a name="step-2-download-the-ata-gateway-setup-package"></a>Steg 2. Hämta installationspaketet för ATA Gateway
När du har konfigurerat anslutningsinställningarna för domänen kan du hämta ATA Gateway-installationspaketet.

För att hämta ATA Gateway-paketet:

1.  Ta bort alla versioner av ATA Gateway-paketet som du har hämtat tidigare.

2.  Öppna en webbläsare på ATA Gateway-datorn och ange IP-adressen som du konfigurerade i ATA Center för ATA-konsolen. När ATA-konsolen öppnas klickar du på inställningsikonen och väljer **Konfiguration**.

    ![Ikon för konfigurationsinställningar](media/ATA-config-icon.png)

3.  På fliken **ATA Gateways** klickar du på **Hämta installationsprogram för ATA Gateway**.

4.  Spara paketet lokalt.

Zip-filen innehåller följande filer:

-   Installationsprogram för ATA Gateway

-   Filen med konfigurationsinställningar som innehåller informationen som krävs för att ansluta till ATA Center

### <a name="step-3-update-the-ata-gateways"></a>Steg 3: Uppdatera ATA Gateways

1.  Extrahera filerna från ATA Gateway-paketet på varje ATA Gateway och kör filen **Microsoft ATA Gateway Setup.exe**.

    > [!NOTE] 
    > Du kan också använda det här ATA Gateway-paketet för att installera nya ATA Gateways.

2.  De tidigare inställningarna bevaras, men det kan ta några minuter innan tjänsten startas om.

3.  Upprepa det här steget för alla andra distribuerade ATA Gateways.

> [!NOTE] 
> När en uppdatering av en ATA Gateway är klar försvinner meddelandet om att den är föråldrad på den specifika ATA-gatewayen.

Du vet att alla ATA-gatewayer har uppdaterats när alla ATA Gateways rapporterar att synkroniseringen är klar och meddelandet att ett uppdaterat ATA Gateway-paketet är tillgänglig visas inte längre.

![Bild av uppdaterade gateways](media/ATA-gw-updated.png)


## <a name="see-also"></a>Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
