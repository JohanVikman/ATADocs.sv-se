---
title: "Migreringsguide för Advanced Threat Analytics-uppdatering till 1.5 | Microsoft Docs"
description: "Procedurer för att uppdatera ATA till version 1.5"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 654312c841c38c86c9efa826227d7cc93eb772cf
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2017
---
# <a name="ata-update-to-15-migration-guide"></a>Migreringsguide för ATA-uppdatering till 1.5
Uppdateringen till ATA 1.5 erbjuder förbättringar inom följande områden:

-   Snabbare identifiering

-   Förbättrad automatisk identifieringsalgoritm för NAT-enheter (Network address translation)

-   Förbättrad namnmatchningsprocess för icke-domänanslutna enheter

-   Stöd för migrering av data vid produktuppdateringar

-   Bättre gränssnittssvarstid för misstänkta aktiviteter när tusentals entiteter är inblandade

-   Förbättrad automatisk lösning för övervakningsvarningar

-   Ytterligare prestandaräknare för förbättrad övervakning och felsökning

## <a name="updating-ata-to-version-15"></a>Uppdatera ATA till version 1.5
> [!NOTE]
> Om ATA inte är installerat i din miljö kan du hämta den fullständiga versionen av ATA, som innehåller version 1.5 och följa standardproceduren för installation som beskrivs i [installera ATA](install-ata-step1.md).

Om du redan har distribuerat ATA version 1.4 vägleder dig genom stegen för att uppdatera installationen i den här proceduren.

Följ dessa steg för att uppdatera till ATA-version 1.5:

1.  Hämta ATA v1.5 från VLSC eller MSDN.
      > [!NOTE]
         Du kan även använda den uppdaterade fullständiga versionen av ATA för att uppdatera till version 1.5.


2.  Uppdatera ATA Center

3.  Hämta det uppdaterade Gateway-paketet för ATA

4.  Uppdatera ATA Gateways

    > [!IMPORTANT]
    > Uppdatera alla ATA Gateways för att säkerställa att ATA fungerar korrekt.

### <a name="step-1-update-the-ata-center"></a>Steg 1: Uppdatera ATA Center

1.  Säkerhetskopiera databasen: (valfritt)

    -   Om ATA Center körs som en virtuell dator och du vill ta en kontrollpunkt, stänga av den virtuella datorn först.

    -   Om ATA Center körs på en fysisk server ska du följa den rekommenderade proceduren för att [säkerhetskopiera MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Kör uppdateringsfilen, Microsoft ATA Center Update.exe, och följ anvisningarna på skärmen för att installera uppdateringen.

    1.  På **Välkomstsidan** väljer du språk och klickar på **Nästa**.

    2.  Läs licensavtalet och om du accepterar villkoren klickar du på kryssrutan och klickar på **nästa**.

    3.  Välj om du vill köra fullständig (standard) eller partiell migrering.

        ![Välj fullständig eller partiell migrering](media/ATA-center-fullpartial.png)

        -   Om du väljer **partiella** migreringen all nätverkstrafik som samlas in och vidarebefordrade Windows-händelser som analyserats av ATA tas bort och profiler över användarbeteende måste vara relearned, vilket tar minst tre veckor. Om du har ont om ledigt diskutrymme så är det bra att köra en **partiella** migrering.

        -   Om du kör en **fullständig** migrering, behöver du ytterligare diskutrymme, som beräknas åt dig på sidan uppgradering och migrering kan ta längre tid beroende på nätverkstrafiken. Vid fullständig migrering behålls alla tidigare insamlade data och användarbeteendeprofiler bevaras, vilket innebär att det inte tar någon extra tid för ATA lära in beteendeprofiler och avvikande beteenden kan upptäckas omedelbart efter uppdateringen.

3.  Klicka på **Uppdatera**. När du klickar på Uppdatera är ATA offline tills uppdateringsproceduren har slutförts.

4.  När du har uppdaterat ATA Center rapporterar ATA Gateways att de nu är föråldrade.

    ![Bild av föråldrade gateways](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - Uppdatera alla ATA Gateways för att säkerställa att ATA fungerar korrekt.

### <a name="step-2-download-the-ata-gateway-setup-package"></a>Steg 2. Hämta installationspaketet för ATA Gateway
När du har konfigurerat anslutningsinställningarna för domänen kan du hämta ATA Gateway-installationspaketet.

Hämta ATA Gateway-paketet:

1.  Ta bort alla versioner av ATA Gateway-paketet som du har hämtat tidigare.

2.  Öppna en webbläsare på ATA Gateway-datorn och ange IP-adressen som du konfigurerade i ATA Center för ATA-konsolen. När ATA-konsolen öppnas klickar du på inställningsikonen och väljer **Konfiguration**.

    ![Ikon för konfigurationsinställningar](media/ATA-config-icon.png)

3.  På fliken **ATA Gateways** klickar du på **Hämta installationsprogram för ATA Gateway**.

4.  Spara paketet lokalt.

Zip-filen innehåller följande filer:

-   Installationsprogram för ATA Gateway

-   Filen med konfigurationsinställningar som innehåller informationen som krävs för att ansluta till ATA Center

### <a name="step-3-update-the-ata-gateways"></a>Steg 3: Uppdatera ATA Gateways

1.  Extrahera filerna från ATA Gateway-paketet på varje ATA Gateway och kör filen Microsoft ATA Gateway Setup.

    > [!NOTE]
    > Du kan också använda det här ATA Gateway-paketet för att installera nya ATA Gateways.

2.  De tidigare inställningarna bevaras, men det kan ta några minuter innan tjänsten startas om.

3.  Upprepa det här steget för alla andra distribuerade ATA Gateways.

> [!NOTE]
> När en uppdatering av en ATA Gateway är klar försvinner meddelandet om att den är föråldrad på den specifika ATA Gatewayen.

Du vet att uppdateringen av alla ATA Gateways är klar när alla ATA Gateways rapporterar att synkroniseringen är klar och genom att meddelandet om att det finns ett uppdaterat ATA Gateway-paket inte längre visas.

![Bild av uppdaterade gateways](media/ATA-gw-updated.png)

## <a name="see-also"></a>Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
