---
title: "Ändra ATA-konfiguration – lösenord för domänanslutning | Microsoft ATA"
description: "Beskriver hur du ändrar lösenordet för domänanslutning på ATA-gatewayen."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 050f1ef0b39d69b64ede53243a7fa2d33d0e4813
ms.openlocfilehash: 7cee457a8959526b25a68c50efea2976bafbef75


---

*Gäller för: Advanced Threat Analytics version 1.7*



# Ändra ATA-konfiguration – lösenord för domänanslutning

>[!div class="step-by-step"]
[« ATA-konsolens URL](modifying-ata-config-consoleurl.md)


## Ändra lösenord för domänanslutning
Om du ändrar lösenordet för domänanslutning ska du se till att lösenordet du anger stämmer. Om det inte stämmer stoppas ATA Gateway-tjänsten på ATA-gatewayerna.

Om du misstänker att det har inträffat tittar du efter följande i filen Microsoft.Tri.Gateway Errors.log på ATA-gatewayen:
`The supplied credential is invalid.`

Du åtgärdar det genom att följa den här proceduren för att uppdatera lösenordet för domänanslutning på ATA-Center:

1.  Öppna ATA-konsolen på ATA Center.

2.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.JPG)

3.  Välj **Katalogtjänster**.

    ![Bild av hur du ändrar lösenord i ATA Gateway](media/ATA-GW-change-DC-password.png)

4.  Under **Lösenord**, ändrar du lösenordet.

    Om ATA Center har anslutning till domänen, använder du knappen **Testa anslutning** för att verifiera autentiseringsuppgifterna

5.  Klicka på **Spara**.

6.  När du har ändrat lösenordet ska du manuellt kontrollera att ATA Gateway-tjänsten körs på ATA Gateway-servrarna.

>[!div class="step-by-step"]
[« ATA-konsolens URL](modifying-ata-config-consoleurl.md)

## Se även
- [Arbeta med ATA-konsolen](working-with-ata-console.md)
- [Installera ATA](install-ata.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


