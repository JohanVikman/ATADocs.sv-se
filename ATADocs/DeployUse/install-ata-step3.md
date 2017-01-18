---
title: "Installera ATA – Steg 3 | Microsoft Docs"
description: "Steg tre av ATA-installationen hjälper dig att hämta installationspaketet för ATA Gateway."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: c8f3f5453757fbc7a95aa2377a84c3a133d38181


---

*Gäller för: Advanced Threat Analytics version 1.7*



# <a name="install-ata---step-3"></a>Installera ATA – Steg 3

>[!div class="step-by-step"]
[« Steg 2](install-ata-step2.md)
[Steg 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>Steg 3. Hämta installationspaketet för ATA Gateway
När du har konfigurerat anslutningsinställningarna för domänen kan du hämta ATA Gateway-installationspaketet. ATA Gateway kan installeras på dedikerad server eller en domänkontrollant. Om du installerar den på en domänkontrollant kommer den att installeras som en ATA Lightweight Gateway. Mer information om ATA Lightweight Gateway finns i [ATA-arkitektur](/advanced-threat-analytics/plan-design/ata-architecture). 

Om det är första gången du hämtar en ATA Gateway visas följande skärm:

![Konfigurationsinställningar för ATA Gateway](media/ATA_1.7-welcome-download-gateway.PNG)

Välkomstmeddelandet visas inte om det inte är första gången du hämtar en ATA Gateway.

> [!NOTE] 
> För att nå konfigurationsskärmen senare, klickar du på **inställningsikonen** (uppe till höger) och väljer **Konfiguration**, under **System**, klickar du sedan på **Gateways**.  

1.  Klicka på **"Hämta Gateway-installation"**.
2.  Spara paketet lokalt.
3.  Kopiera paketet till den dedikerade servern eller domänkontrollanten där du installerar ATA Gateway. Du kan även öppna ATA-konsolen från den dedikerade servern eller domänkontrollanten och hoppa över detta steg.

ZIP-filen innehåller följande:

-   Installationsprogram för ATA Gateway

-   Filen med konfigurationsinställningar som innehåller informationen som krävs för att ansluta till ATA Center


>[!div class="step-by-step"]
[« Steg 2](install-ata-step2.md)
[Steg 4 »](install-ata-step4.md)

## <a name="see-also"></a>Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Jan17_HO1-->


