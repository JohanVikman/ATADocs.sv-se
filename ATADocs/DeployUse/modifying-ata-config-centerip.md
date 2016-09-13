---
title: "Ändra ATA-konfiguration – IP-adress för ATA Center | Microsoft ATA"
description: "Beskriver hur du ändrar IP-adress, port eller certifikat för ett ATA Center."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 93b27f15-f7e5-49bb-870a-d81d09dfe9fc
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: e6d42610d1c785da5b7c7b1cf035d94c2fddff4b


---

*Gäller för: Advanced Threat Analytics version 1.7*



# Ändra ATA-konfiguration – IP-adress för ATA Center

>[!div class="step-by-step"]
[ATA Center-certifikat »](modifying-ata-config-centercert.md)

Efter den första distributionen bör ändringar i ATA Center genomföras med försiktighet. Använd följande procedurer när du uppdaterar IP-adressen och porten eller certifikatet.

## Ändra IP-adressen som används av ATA Center-servern
Ta hänsyn till följande om du behöver ändra IP-adress och port eller certifikat för ATA Center.

ATA Gateways lagrar IP-adressen till det ATA Center de behöver ansluta till lokalt. De ansluter regelbundet till ATA Center och hämtar konfigurationsändringar. Det är en process i två steg att ändra hur en ATA Gateway ansluter till ATA Center.

-   Steg ett: uppdatera IP-adressen och porten du vill att ATA Center-tjänsten ska använda. I det här läget lyssnar ATA Center fortfarande på den ursprungliga IP-adressen och nästa gång ATA Gateway synkroniserar sin konfiguration får den två IP-adresser till ATA Center. Så länge ATA Gateway kan ansluta genom att använda den ursprungliga (första) IP-adressen kommer den inte att försöka använda den nya IP-adressen och porten.

-   Steg två: när alla ATA Gateways har synkroniserats med den uppdaterade konfigurationen ska den nya IP-adressen och porten som ATA Center lyssnar på aktiveras. När du aktiverar den nya IP-adressen kopplas ATA Center-tjänsten till denna. ATA Gateways kommer inte att kunna ansluta till den ursprungliga adressen och försöker nu att ansluta till den andra (nya) IP-adressen till ATA Center. Efter anslutning till ATA Center med den nya IP-adressen hämtar ATA Gateway den senaste konfigurationen och har en enda IP-adress för ATA Center. (Såvida du inte startade processen igen.)

> [!NOTE]
> -   Om en ATA Gateway var offline under det första steget och aldrig fick den uppdaterade konfigurationen måste du uppdatera konfigurationens JSON-fil manuellt på ATA Gatewayen.
> -   Om den nya IP-adressen är installerad på ATA Center-servern kan du välja den i listan med IP-adresser när ändringen genomförs. Om du av någon anledning inte kan installera IP-adressen på ATA Center-servern kan du välja en anpassad IP-adress och lägga till denna manuellt. Du kan inte aktivera den nya IP-adressen innan den har installerats på servern.
> -   Om du behöver distribuera en ny ATA Gateway efter aktivering av den nya IP-adressen måste du hämta konfigurationspaketet för ATA Gateway igen.

1.  Öppna ATA-konsolen.

2.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.JPG)

3.  Välj **Center**.

4.  Under ** IP-adress för Center-tjänst: port** väljer du någon av de befintliga IP-adresserna eller **Lägg till anpassad IP-adress** och anger en IP-adress.

5.  Klicka på **Spara**.

6.  Ett meddelande om hur många ATA Gateways som har synkats med den senaste konfigurationen visas.

    ![Bild på synkroniserade ATA Center Gateways](media/ATA-chge-IP-after-clicking-save.png)

    >[!IMPORTANT]
    >Verifiera att alla ATA-gatewayer synkroniseras med den senaste konfigurationen innan du aktiverar den nya konfigurationen. Om den nya konfigurationen aktiveras innan alla ATA-gatewayer har synkroniserats kan ATA Gateway sluta att fungera som förväntat. Om någon ATA Gateway inte är synkroniserad får du det här felet när du klickar på Aktivera:
    >
    >    ![Synkroniseringsfel för ATA Gateway](media/ataGW-not-synced.png)


7.  När alla ATA Gateways har synkroniserats klickar du på **Aktivera** för att aktivera den nya IP-adressen.

    > [!NOTE]
    > Om du har angett en anpassad IP-adress går det inte att klicka på **Aktivera** förrän du har installerat den IP-adressen på ATA Center.

8.  Se till att alla ATA Gateways kan synkronisera sina konfigurationer efter att ändringen har aktiverats. Meddelandefältet visar hur många ATA Gateway-konfigurationer som synkroniserats.

>[!div class="step-by-step"]
[Ändra ATA Center-certifikatet »](modifying-ata-config-centercert.md)


## Se även
- [Arbeta med ATA-konsolen](working-with-ata-console.md)
- [Installera ATA](install-ata.md)
- [Ta en titt i ATA-forumet!](https://aka.ms/ata-forum)



<!--HONumber=Aug16_HO5-->


