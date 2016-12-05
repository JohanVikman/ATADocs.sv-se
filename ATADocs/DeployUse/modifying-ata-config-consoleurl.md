---
title: "Ändra ATA-konfiguration – IP-adress för ATA-konsolen | Microsoft Advanced Threat Analytics"
description: "Beskriver hur du ändrar IP-adressen för ATA-konsolen, som används för att skapa en genväg till ATA-konsolen på ATA-gatewayerna."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: stevenpo
ms.date: 11/29/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: bc7af91a925928183d179391f15d3a24cda2b576
ms.openlocfilehash: 8f816c8eda0a1b11a42314a18b1c8c39ac6a7ba8


---

*Gäller för: Advanced Threat Analytics version 1.7*



# <a name="change-ata-configuration---ata-console-url"></a>Ändra ATA-konfiguration – URL för ATA-konsolen

>[!div class="step-by-step"]
[« ATA Center-certifikat](modifying-ata-config-centercert.md)
[Lösenord för domänanslutning »](modifying-ata-config-dcpassword.md)

## <a name="change-the-ata-console-url"></a>Ändra ATA-konsolens URL
ATA-konsolens URL är som standard den IP-adress som valdes som IP-adress för ATA-konsolen när du installerade ATA Center.

URL:en används i följande scenarier:

-   Installation av ATA-gatewayer – när en ATA-gateway installeras registreras den i ATA Center. Registreringen utförs genom att ansluta till ATA-konsolen. Om du anger ett FQDN som ATA-konsolens URL måste du se till att ATA-gatewayen kan matcha detta FQDN till IP-adressen som ATA-konsolen är bunden till.

-   Aviseringar – när ATA skickar ut en SIEM- eller e-postavisering innehåller den en länk till den misstänkta aktiviteten. Värddelen av länken är URL-inställningen i ATA-konsolen.

-   Om du har installerat ett certifikat från din interna certifikatutfärdare (CA) bör du matcha URL:en till ämnesnamnet i certifikatet så att användarna inte får ett varningsmeddelande när de ansluter till ATA-konsolen.

-   Med ett FQDN som ATA-konsolens URL kan du ändra IP-adressen som används av ATA-konsolen utan att förstöra aviseringar som har skickats tidigare eller behöva ladda ned ATA Gateway-paketet igen. Du behöver bara uppdatera DNS med den nya IP-adressen.

> [!NOTE]
> När du har ändrat ATA-konsolens URL bör du ladda ned installationspaketet för ATA Gateway innan du installerar nya ATA-gatewayer.

Följ de här stegen på ATA Center-servern om du behöver ändra URL för ATA-konsolen.

1.  Öppna ATA-konsolen.

2.  Välj inställningsalternativ i verktygsfältet och välj **Konfiguration**.

    ![Ikon för ATA-konfigurationsinställningar](media/ATA-config-icon.JPG)

3.  Välj **Center**.

4.  Under **Konsolens IP-adress**, väljer du någon av de befintliga IP-adresserna

5.  Under **Konsol-URL**, ändra webbadressen efter behov:

    ![ATA-konsolens URL](media/ATA-chge-center-URL.png)
> [!NOTE]
> Inkludera inte snedstreck / i slutet av URL:en.

6.  Klicka på **Spara**.

>[!div class="step-by-step"]
[« ATA Center-certifikat](modifying-ata-config-centercert.md)
[Lösenord för domänanslutning »](modifying-ata-config-dcpassword.md)


## <a name="see-also"></a>Se även
- [Arbeta med ATA-konsolen](working-with-ata-console.md)
- [Ta en titt i ATA-forumet!](https://aka.ms/ata-forum)



<!--HONumber=Nov16_HO5-->


