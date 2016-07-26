---
title: "Ändra ATA-konfiguration – IIS-certifikat | Microsoft ATA"
description: "Beskriver hur du ändrar certifikatet som används av IIS för ATA Center."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: e58a0390-57ef-4c68-a987-2e75e5f3d6b3
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 6516500f3134228cc92e269ef5ea8bfe4faa19d9


---

# Ändra ATA-konfiguration – IIS-certifikat

>[!div class="step-by-step"]
[« ATA-konsolens IP-adress](modifying-ata-config-consoleip.md)
[Lösenord för domänanslutning »](modifying-ata-config-dcpassword.md)

## Ändra IIS-certifikatet
I konsolen kan du markera och ändra certifikatet för ATA Center-tjänsten, men du kan inte ändra certifikatet som används av IIS.

Gör så här om du vill ändra det:

> [!NOTE]
> När du har ändrat IIS-certifikatet bör du hämta installationspaketet för ATA Gateway innan du installerar nya ATA-gatewayer.

Följ de här stegen från ATA Center-servern om du behöver ändra certifikatet som används av IIS för ATA Center.

1.  Installera det nya certifikatet på ATA Center-servern.

2.  Öppna IIS-hanteraren (Internet Information Services).A

3.  Expandera namnet på servern och **Platser**.

4.  Välj platsen för Microsoft ATA-konsolen, gå till rutan **Åtgärder** och klicka på **Bindningar**.

    ![Åtgärder för ATA-konsolens bindningar](media/ATA-console-change-IP-bindings.jpg)

5.  Välj **HTTPS** och klicka på **Redigera**.

6.  Under **SSL-certifikat** väljer du det nya certifikatet.

7.  Hämta installationspaketet för ATA Gateway innan du installerar en ny ATA Gateway.

>[!div class="step-by-step"]
[« ATA-konsolens IP-adress](modifying-ata-config-consoleip.md)
[Lösenord för domänanslutning »](modifying-ata-config-dcpassword.md)

## Se även
- [Arbeta med ATA-konsolen](working-with-ata-console.md)
- [Installera ATA](install-ata.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


