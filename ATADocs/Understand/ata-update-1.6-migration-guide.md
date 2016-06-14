---
# required metadata

title: Migreringsguide för ATA-uppdatering till 1.6 | Microsoft Advanced Threat Analytics
description: Procedurer för att uppdatera ATA till version 1.6
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

# Migreringsguide för ATA-uppdatering till 1.6
Uppdateringen för ATA 1.6 ger förbättringar inom följande områden:

-   Nya identifieringar

-   Förbättringar av befintliga identifieringar

-   ATA Lightweight Gateway

-   Automatiska uppdateringar

-   Förbättrad prestanda för ATA Center

-   Lägre lagringskrav

-   Stöd för IBM QRadar

## Uppdatera ATA till version 1.6
> [!NOTE] Om ATA inte är installerat i miljön kan du hämta den fullständiga versionen av ATA, som innehåller version 1.6, och följa standardproceduren för installation som beskrivs i [Installera ATA](/advanced-threat-analytics/deploy-use/install-ata).

Om du redan har distribuerat ATA version 1.5 vägleder den här proceduren dig igenom de steg som krävs för att uppdatera distributionen.

> [!NOTE] Du kan inte installera ATA version 1.6 direkt på ATA version 1.4. Du måste först installera ATA version 1.5. Om du av misstag har försökt installera ATA 1.6 utan att installera ATA 1.5 visas ett fel som säger att **En nyare version är redan installerad på datorn.** Du måste avinstallera resterna av ATA 1.6 som är kvar på datorn, trots att installationen misslyckades, innan du installerar ATA version 1.5.

Följ dessa steg för att uppdatera till ATA version 1.6:

1. Innan du startar uppgraderingsprocessen ser du till att följa metoden för att hantera [Migreringsfel vid uppdatering till ATA version 1.6](whats-new-version-1.6#Migration-failure-when-updating-from-ATA-1.5)
2. Kontrollera att du har det lediga utrymme som krävs för att slutföra uppgraderingen. Du kan utföra installationen fram till beredskapskontrollen för att få en beräkning av hur mycket ledigt utrymme som krävs, och sedan starta om uppgraderingen efter att det nödvändiga diskutrymmet har tilldelats. Uppgraderingen använder minst 2 % av databasstorleken, mer information finns i [ATA-kapacitetsplanering](/advanced-threat-analytics/plan-design/ata-capacity-planning).
1.  [Hämta uppdateringen 1.6](http://www.microsoft.com/en-us/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
I den här versionen används samma installationsfil (Microsoft ATA Center Setup.exe) för att installera en ny distribution av ATA och för att uppgradera befintliga distributioner.

2.  Uppdatera ATA Center

3.  Hämta det uppdaterade Gateway-paketet för ATA

4.  Uppdatera ATA Gateways

    > [!IMPORTANT] Uppdatera alla ATA-gatewayer för att säkerställa att ATA fungerar korrekt.

### Steg 1: Uppdatera ATA Center

1.  Säkerhetskopiera databasen: (valfritt)

    -   Om ATA Center körs som en virtuell dator och du vill göra en kontrollpunkt ska du först stänga av den virtuella datorn.

    -   Om ATA Center körs på en fysisk server ska du följa den rekommenderade proceduren för att [säkerhetskopiera MongoDB](https://docs.mongodb.org/manual/core/backups/).

2.  Kör installationsfilen, Microsoft ATA Center Setup.exe, och följ anvisningarna på skärmen för att installera uppdateringen.

    1.  ATA 1.6 kräver att .Net Framework 4.6.1 är installerat. Om det inte redan är installerat kommer ATA-installationen att installera .Net Framework 4.6.1 som en del av installationen<br>
    > [!NOTE]Installationen av .Net Framework 4.6.1 kan kräva att servern startas om. ATA-installationen fortsätter först efter att servern har startats om.
5.  På sidan **Välkommen** väljer du språk och klickar på **Nästa**.

    6.  Läs licensavtalet och klicka på **Nästa** om du godkänner licensvillkoren.

    7.  Det är nu möjligt att använda Microsoft Update för att hålla ATA uppdaterat.  På sidan Microsoft Update markerar du **Använd Microsoft Update när jag söker efter uppdateringar (rekommenderas)**.
    ![Bild för att hålla ATA uppdaterat](media/ata_ms_update.png) Detta justerar Windows-inställningarna för att aktivera uppdateringar för andra Microsoft-produkter (inklusive ATA), på det sätt som visas här. 
     ![Bild för automatisk uppdatering av Windows](media/ata_installupdatesautomatically.png)

    8.  ATA utför en beredskapskontroll innan installationen påbörjas. Granska resultaten av kontrollen för att se till att kraven har konfigurerats och du har det minsta tillgängliga diskutrymme som krävs. 
    ![Bild för ATA-beredskapskontroll](media/ata_install_readinesschecks.png)

    3.  Klicka på **Uppdatera**. När du har klickat på Uppdatera är ATA offline tills uppdateringsproceduren har slutförts.

4.  När du har uppdaterat ATA Center rapporterar ATA Gateways att de nu är föråldrade.

    ![Bild av föråldrade gateways](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - Uppdatera alla ATA Gateways för att säkerställa att ATA fungerar korrekt.

### Steg 2. Hämta installationspaketet för ATA Gateway
När du har konfigurerat anslutningsinställningarna för domänen kan du hämta ATA Gateway-installationspaketet.

Hämta ATA Gateway-paketet:

1.  Ta bort alla versioner av ATA Gateway-paketet som du har hämtat tidigare.

2.  Öppna en webbläsare på ATA Gateway-datorn och ange IP-adressen som du konfigurerade i ATA Center för ATA-konsolen. När ATA-konsolen öppnas klickar du på inställningsikonen och väljer **Konfiguration**.

    ![Ikon för konfigurationsinställningar](media/ATA-config-icon.JPG)

3.  På fliken **ATA Gateways** klickar du på **Hämta installationsprogram för ATA Gateway**.

4.  Spara paketet lokalt.

ZIP-filen innehåller följande:

-   Installationsprogram för ATA Gateway

-   Filen med konfigurationsinställningar som innehåller informationen som krävs för att ansluta till ATA Center

### Steg 3: Uppdatera ATA Gateways

1.  Extrahera filerna från ATA Gateway-paketet på varje ATA Gateway och kör filen **Microsoft ATA Gateway Setup.exe**.

    > [!NOTE] Du kan också använda det här ATA Gateway-paketet för att installera nya ATA-gatewayer.

2.  De tidigare inställningarna bevaras, men det kan ta några minuter för tjänsten att startas om.

3.  Upprepa det här steget för alla andra distribuerade ATA Gateways.

> [!NOTE] När en uppdatering av en ATA Gateway är klar försvinner meddelandet om att den är föråldrad på den specifika ATA-gatewayen.

Du vet att uppdateringen av alla ATA Gateways är klar när alla ATA Gateways rapporterar att synkroniseringen är klar och genom att meddelandet om att det finns ett uppdaterat ATA Gateway-paket inte längre visas.

![Bild av uppdaterade gateways](media/ATA-gw-updated.png)


## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO4-->


