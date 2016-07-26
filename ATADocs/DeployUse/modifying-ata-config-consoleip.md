---
title: "Ändra ATA-konfiguration – IP-adress för ATA-konsol | Microsoft ATA"
description: "Beskriver hur du ändrar IP-adressen för ATA-konsolen, som används för att skapa en genväg till ATA-konsolen på ATA-gatewayerna."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 50118465-df34-4e04-b0cc-48808b6a96b1
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 3c02459e6a0cde359e632bf966948cf3a72170a2


---

# Ändra ATA-konfiguration – IP-adress för ATA-konsolen

>[!div class="step-by-step"]
[«ATA Center-certifikat](modifying-ata-config-centercert.md)
[IIS-certifikat»](modifying-ata-config-iiscert.md)

## Ändra IP-adressen för ATA-konsolen
ATA-konsolens URL är som standard den IP-adress som valdes som IP-adress för ATA-konsolen när du installerade ATA Center.

URL:en används i följande scenarier:

-   Installation av ATA-gatewayer – när en ATA-gateway installeras registreras den i ATA Center. Registreringen utförs genom att ansluta till ATA-konsolen. Om du anger ett FQDN som ATA-konsolens URL måste du se till att ATA-gatewayen kan matcha detta FQDN till IP-adressen som ATA-konsolen är bunden till i IIS. Dessutom används URL:en för att skapa genvägen till ATA-konsolen på ATA-gatewayerna.

-   Aviseringar – när ATA skickar ut en SIEM- eller e-postavisering innehåller den en länk till den misstänkta aktiviteten. Värddelen av länken är URL-inställningen i ATA-konsolen.

-   Om du har installerat ett certifikat från din interna certifikatutfärdare (CA) bör du matcha URL:en till ämnesnamnet i certifikatet så att användarna inte får ett varningsmeddelande när de ansluter till ATA-konsolen.

-   Med ett FQDN som ATA-konsolens URL kan du ändra IP-adressen som används av IIS för ATA-konsolen utan att förstöra aviseringar som har skickats tidigare eller behöva ladda ned ATA Gateway-paketet igen. Du behöver bara uppdatera DNS med den nya IP-adressen.

> [!NOTE]
> När du har ändrat ATA-konsolens URL bör du ladda ned installationspaketet för ATA Gateway innan du installerar nya ATA-gatewayer.

Följ de här stegen på ATA Center-servern om du behöver ändra IP-adressen som används av IIS för ATA-konsolen.

1.  Installera IP-adressen på ATA Center-servern.

2.  Öppna IIS-hanteraren (Internet Information Services).

3.  Expandera namnet på servern och **Platser**.

4.  Välj platsen för Microsoft ATA-konsolen, gå till rutan **Åtgärder** och klicka på **Bindningar**.

    ![Bild av åtgärder för ATA-konsolens bindningar](media/ATA-console-change-IP-bindings.jpg)

5.  Välj **HTTP**, klicka på **Redigera** och välj den nya IP-adressen. Gör samma sak för **HTTPS** och välj samma IP-adress.

    ![Bild av Redigera bindning för webbplats](media/ATA-change-console-IP.jpg)

6.  I rutan **Åtgärd** klickar du på **Starta om** under **Hantera webbplats**.

7.  Öppna en administratörskommandotolk och skriv följande kommandon för att uppdatera HTTP.SYS-drivrutinen:

    -   Om du vill lägga till den nya IP-adressen – `netsh http add iplisten ipaddress=newipaddress`

    -   Om du vill se att den nya adressen används – `netsh http show iplisten`

    -   Om du vill ta bort den gamla IP-adressen – `netsh http delete iplisten ipaddress=oldipaddress`

8.  Om ATA-konsolens URL fortfarande använder en IP-adress uppdaterar du ATA-konsolens URL till den nya IP-adressen och laddar ned installationspaketet för ATA Gateway innan du distribuerar nya ATA-gatewayer.

9. Om ATA-konsolens URL är ett FQDN uppdaterar du DNS med den nya IP-adressen för FQDN.

>[!div class="step-by-step"]
[«ATA Center-certifikat](modifying-ata-config-centercert.md)
[IIS-certifikat»](modifying-ata-config-iiscert.md)


## Se även
- [Arbeta med ATA-konsolen](working-with-ata-console.md)
- [Installera ATA](install-ata.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


