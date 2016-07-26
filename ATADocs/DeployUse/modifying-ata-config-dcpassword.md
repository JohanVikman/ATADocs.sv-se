---
title: "Ändra ATA-konfiguration – lösenord för domänanslutning | Microsoft ATA"
description: "Beskriver hur du ändrar lösenordet för domänanslutning på ATA-gatewayen."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 860a83aa4e6656480217a457bb2492431d73637a


---

# Ändra ATA-konfiguration – lösenord för domänanslutning

>[!div class="step-by-step"]
[« IIS-certifikat](modifying-ata-config-iiscert.md)


## Ändra lösenord för domänanslutning
Om du ändrar lösenordet för domänanslutning ska du se till att lösenordet du anger stämmer. Om det inte stämmer stoppas ATA Gateway-tjänsten på ATA-gatewayerna.

Om du misstänker att det har inträffat tittar du efter följande i filen Microsoft.Tri.Gateway Errors.log på ATA-gatewayen:
`The supplied credential is invalid.`

Du åtgärdar det genom att följa den här proceduren för att uppdatera lösenordet för domänanslutning på ATA-gatewayen:

1.  Öppna ATA-konsolen på ATA-gatewayen.

2.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.JPG)

3.  Välj **Allmänt**.

    ![Bild av hur du ändrar lösenord i ATA Gateway](media/ATA-GW-change-DC-password.JPG)

4.  Ändra lösenordet under **Allmänt**.

5.  Klicka på **Spara**.

6.  När du har ändrat lösenordet ska du manuellt kontrollera att ATA Gateway-tjänsten körs på ATA Gateway-servrarna.

>[!div class="step-by-step"]
[« IIS-certifikat](modifying-ata-config-iiscert.md)

## Se även
- [Arbeta med ATA-konsolen](working-with-ata-console.md)
- [Installera ATA](install-ata.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


