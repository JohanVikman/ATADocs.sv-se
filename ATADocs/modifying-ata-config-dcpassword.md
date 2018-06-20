---
title: Ändra Advanced Threat Analytics-konfigurationen – lösenord för domänanslutning | Microsoft Docs
description: Beskriver hur du ändrar lösenordet för domänanslutning på ATA-gatewayen.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 4a25561b-a5ed-44aa-9b72-366976b3c72a
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 47bd7e9cdd97d8343202be86954e82e69948afed
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009317"
---
*Gäller för: Advanced Threat Analytics version 1.9.*



# <a name="change-ata-configuration---domain-connectivity-password"></a>Ändra ATA-konfiguration – lösenord för domänanslutning



## <a name="change-the-domain-connectivity-password"></a>Ändra lösenord för domänanslutning
Om du ändrar lösenordet för domänanslutning ska du se till att lösenordet du anger stämmer. Om det inte är stoppas ATA Gateway-tjänsten körs på ATA-gatewayer.

Om du misstänker att det har inträffat på ATA-Gateway kan du titta på filen Microsoft.Tri.Gateway-Errors.log för följande fel: `The supplied credential is invalid.`

Du åtgärdar det genom att följa den här proceduren för att uppdatera lösenordet för domänanslutning på ATA-Center:

1.  Öppna ATA-konsolen på ATA Center.

2.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.png)

3.  Välj **Katalogtjänster**.

    ![Bild av hur du ändrar lösenord i ATA Gateway](media/ATA-GW-change-DC-password.png)

4.  Under **Lösenord**, ändrar du lösenordet.

    Om ATA Center har anslutning till domänen använder den **Testanslutningen** för att verifiera autentiseringsuppgifterna

5.  Klicka på **Spara**.

6.  När du har ändrat lösenordet ska du manuellt kontrollera att ATA Gateway-tjänsten körs på ATA Gateway-servrarna.



## <a name="see-also"></a>Se även
- [Arbeta med ATA-konsolen](working-with-ata-console.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
