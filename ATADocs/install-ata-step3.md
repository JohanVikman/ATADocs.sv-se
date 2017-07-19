---
title: Installera Advanced Threat Analytics steg 3 | Microsoft Docs
description: "Steg tre av ATA-installationen hjälper dig att hämta installationspaketet för ATA Gateway."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/12/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 68c169ffd0f42bd8b030dc12f4711cbde2718a99
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/30/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="install-ata---step-3"></a>Installera ATA – Steg 3

>[!div class="step-by-step"]
[« Steg 2](install-ata-step2.md)
[Steg 4 »](install-ata-step4.md)

## <a name="step-3-download-the-ata-gateway-setup-package"></a>Steg 3. Hämta installationspaketet för ATA Gateway
När du har konfigurerat anslutningsinställningarna för domänen kan du hämta ATA Gateway-installationspaketet. ATA Gateway kan installeras på dedikerad server eller en domänkontrollant. Om du installerar den på en domänkontrollant kommer den att installeras som en ATA Lightweight Gateway. Mer information om ATA Lightweight Gateway finns i [ATA-arkitektur](ata-architecture.md). 

Gå till sidan Gatewayer genom att klicka på Download Gateway Setup (Hämta konfiguration för gateway) i listan med steg överst på sidan:

![Konfigurationsinställningar för ATA Gateway](media/ATA_1.7-welcome-download-gateway.PNG)

> [!NOTE] 
> För att sedan komma till sidan för gatewaykonfiguration klickar du på **inställningsikonen** (uppe till höger) och väljer **Konfiguration** och klickar sedan på **Gatewayer** under **System**.  

1.  Klicka på **Gatewaykonfiguration**.
  ![Download Gateway Setup](media/download-gateway-setup.png) (Hämta konfiguration för ATA Gateway)
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
- [Krav för ATA](ata-prerequisites.md)
