---
# required metadata

title: Migreringsguide för ATA-uppdatering till 1.5 | Microsoft Advanced Threat Analytics
description: Procedurer för att uppdatera ATA till version 1.5
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Migreringsguide för ATA-uppdatering till 1.5
Uppdateringen till ATA 1.5 erbjuder förbättringar inom följande områden:

-   Snabbare identifiering

-   Förbättrad automatisk identifieringsalgoritm för NAT-enheter (Network address translation)

-   Förbättrad namnmatchningsprocess för icke-domänanslutna enheter

-   Stöd för migrering av data vid produktuppdateringar

-   Bättre gränssnittssvarstid för misstänkta aktiviteter när tusentals entiteter är inblandade

-   Förbättrad automatisk lösning för övervakningsvarningar

-   Ytterligare prestandaräknare för förbättrad övervakning och felsökning

## Uppdatera ATA till version 1.5
> [!NOTE]
> Om ATA inte är installerat i miljön kan du hämta den fullständiga versionen av ATA, som innehåller version 1.5, och följa standardproceduren för installation som beskrivs i [Installera ATA](/advanced-threat-analytics/deploy-use/install-ata).

Om du redan har distribuerat ATA version 1.4 vägleder den här proceduren dig igenom de steg spm krävs för att uppdatera installationen.

Följ dessa steg för att uppdatera till ATA-version 1.5:

1.  [Hämta uppdateringen 1.5](http://aka.ms/ata1_5update)
      > [!NOTE]
         Du kan även använda den uppdaterade fullständiga versionen av ATA för att uppdatera till version 1.5.


2.  Uppdatera ATA Center

3.  Hämta det uppdaterade Gateway-paketet för ATA

4.  Uppdatera ATA Gateways

    > [!IMPORTANT]
    > Uppdatera alla ATA Gateways för att säkerställa att ATA fungerar korrekt.

### Steg 1: Uppdatera ATA Center

1.  Säkerhetskopiera databasen: (valfritt)

    -   Om ATA Center körs som en virtuell dator och du vill göra en kontrollpunkt ska du först stänga av den virtuella datorn.

    -   Om ATA Center körs på en fysisk server ska du följa den rekommenderade proceduren för att [säkerhetskopiera MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Kör uppdateringsfilen, Microsoft ATA Center Update.exe, och följ anvisningarna på skärmen för att installera uppdateringen.

    1.  På **Välkomstsidan** väljer du språk och klickar på **Nästa**.

    2.  Läs licensavtalet, markera kryssrutan och klicka på **Nästa** om du godkänner licensvillkoren..

    3.  Välj om du vill köra fullständig (standard) eller partiell migrering.

        ![Välj fullständig eller partiell migrering](media/ATA-center-fullpartial.png)

        -   Om du väljer **partiell** migrering raderas all nätverkstrafik som samlats in och vidarebefordrade Windows-händelser som analyserats av ATA. Profiler över användarbeteende måste då läras in på nytt, vilket tar minst tre veckor. Om du har ont om ledigt diskutrymme så är det bra att köra en **partiell** migrering.

        -   Om du kör en **fullständig** migrering behöver du ytterligare diskutrymme, som beräknas åt dig på sidan för uppgradering, och migreringen kan ta längre tid beroende på nätverkstrafiken. Vid fullständig migrering behålls alla tidigare insamlade data och användarbeteendeprofiler bevaras, vilket innebär att det inte tar någon extra tid för ATA lära in beteendeprofiler och avvikande beteenden kan upptäckas omedelbart efter uppdateringen.

3.  Klicka på **Uppdatera**. När du klickar på Uppdatera är ATA offline tills uppdateringsproceduren har slutförts.

4.  När du har uppdaterat ATA Center rapporterar ATA Gateways att de nu är föråldrade.

    ![Bild av föråldrade gateways](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - Uppdatera alla ATA Gateways för att säkerställa att ATA fungerar korrekt.

### Steg 2. Hämta installationspaketet för ATA Gateways
När du har konfigurerat anslutningsinställningarna för domänen kan du hämta ATA Gateway-installationspaketet.

För att hämta ATA Gateway-paketet:

1.  Ta bort alla versioner av ATA Gateway-paketet som du har hämtat tidigare.

2.  Öppna en webbläsare på ATA Gateway-datorn och ange IP-adressen som du konfigurerade i ATA Center för ATA-konsolen. När ATA-konsolen öppnas klickar du på ikonen för inställningar och väljer **Konfiguration**.

    ![Ikon för konfigurationsinställningar](media/ATA-config-icon.JPG)

3.  På fliken **ATA Gateways** ska du klicka på **Hämta installationsprogram för ATA Gateway**.

4.  Spara paketet lokalt.

ZIP-filen innehåller följande:

-   Installationsprogram för ATA Gateway

-   Filen med konfigurationsinställningar som innehåller informationen som krävs för att ansluta till ATA Center

### Steg 3: Uppdatera ATA Gateways

1.  Extrahera filerna från ATA Gateway-paketet på varje ATA Gateway och kör filen Microsoft ATA Gateway Setup.

    > [!NOTE]
    > Du kan också använda det här ATA Gateway-paketet för att installera nya ATA Gateways.

2.  De tidigare inställningarna bevaras, men det kan ta några minuter innan tjänsten startas om.

3.  Upprepa det här steget för alla andra distribuerade ATA Gateways.

> [!NOTE]
> När en uppdatering av en ATA Gateway är klar försvinner meddelandet om att den är föråldrad på den specifika ATA Gatewayen.

Du vet att uppdateringen av alla ATA Gateways är klar när alla ATA Gateways rapporterar att synkroniseringen är klar och genom att meddelandet om att det finns ett uppdaterat ATA Gateway-paket inte längre visas.

![Bild av uppdaterade gateways](media/ATA-gw-updated.png)

## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


