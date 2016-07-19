---
title: "Ändra ATA-konfiguration – ATA Center-certifikat | Microsoft Advanced Threat Analytics"
description: "Beskriver tvåstegsprocessen för att förnya eller ersätta certifikatet i det lokala datorarkivet på ATA Center-servern."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: c8855287-de3b-4cdd-be8f-2128f48a6f27
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 0cfeb67e663489d7264c88aafe04e77fcb63377f


---

# Ändra ATA-konfiguration – ATA Center-certifikat

>[!div class="step-by-step"]
[«ATA Center-serverns IP-adress](modifying-ata-config-centerip.md)
[ATA-konsolens IP-adress»](modifying-ata-config-consoleip.md)

## Ändra ATA Center-certifikatet
Om certifikaten löper ut och behöver förnyas eller ersättas när det nya certifikatet har installerats i det lokala datorarkivet på ATA Center-servern ersätter du certifikatet genom att följa denna metod i två steg:

-   Första steget – Uppdatera certifikatet som du vill att ATA Center-tjänsten ska använda. ATA Center-tjänsten är då fortfarande kopplad till det ursprungliga certifikatet. När ATA-gatewayerna synkar sin konfiguration har de två möjliga certifikat som är giltiga för ömsesidig autentisering. Så länge ATA-gatewayen kan ansluta med det ursprungliga certifikatet försöker den inte använda det nya.

-   Andra steget – När alla ATA-gatewayer har synkroniserats med den uppdaterade konfigurationen kan du aktivera det nya certifikatet som ATA Center-tjänsten är bunden till. När du aktiverar det nya certifikatet ska ATA Center-tjänsten bindas till certifikatet. ATA-gatewayer kan inte genomföra korrekt ömsesidig autentisering av ATA Center-tjänsten och försöker autentisera det andra certifikatet. Efter anslutning till ATA Center-tjänsten hämtar ATA-gatewayen den senaste konfigurationen och har ett enda certifikat för ATA Center. (Såvida du inte startade processen igen.)

> [!NOTE]
> -   Om en ATA Gateway var offline under det första steget och aldrig fick den uppdaterade konfigurationen måste du uppdatera konfigurationens JSON-fil manuellt på ATA Gatewayen.
> -   Certifikatet som du använder måste vara betrott av ATA-gatewayerna.
> -   Om du behöver distribuera en ny ATA-gateway efter aktivering av det nya certifikatet måste du hämta ATA-gatewaykonfigurationspaketet igen.

1.  Öppna ATA-konsolen.

2.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.JPG)

3.  Välj **ATA Center**.

4.  Under **Certifikat** väljer du något av certifikaten i listan.

5.  Klicka på **Spara**.

6.  Ett meddelande visas om hur många ATA-gatewayer som har synkats till den senaste konfigurationen.

7.  När alla ATA-gatewayer har synkroniserats klickar du på **Aktivera** för att aktivera det nya certifikatet.
    >[!IMPORTANT]
    >Verifiera att alla ATA-gatewayer synkroniseras med den senaste konfigurationen innan du aktiverar den nya konfigurationen. Om den nya konfigurationen aktiveras innan alla ATA-gatewayer har synkroniserats kan ATA Gateway sluta att fungera som förväntat. Om någon ATA Gateway inte är synkroniserad får du det här felet när du klickar på Aktivera:
    >
    >    ![Synkroniseringsfel för ATA Gateway](media/ataGW-not-synced.png)

8.  Se till att alla ATA Gateways kan synkronisera sina konfigurationer efter att ändringen har aktiverats.

>[!div class="step-by-step"]
[«ATA Center-serverns IP-adress](modifying-ata-config-centerip.md)
[ATA-konsolens IP-adress»](modifying-ata-config-consoleip.md)

## Se även
- [Arbeta med ATA-konsolen](working-with-ata-console.md)
- [Installera ATA](install-ata.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


