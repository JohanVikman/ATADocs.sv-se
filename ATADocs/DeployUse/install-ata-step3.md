---
title: "Installera ATA – Steg 3 | Microsoft ATA"
description: "Steg tre av ATA-installationen hjälper dig att hämta installationspaketet för ATA Gateway."
keywords: 
author: rkarlin
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
ms.sourcegitcommit: ba090fdd4f00c001020b1fbedf527e4fd69d3992
ms.openlocfilehash: 277d08756b456d1a61fb9fdcb5014a6a1b4782ad


---

*Gäller för: Advanced Threat Analytics version 1.7*



# Installera ATA – Steg 3

>[!div class="step-by-step"]
[« Steg 2](install-ata-step2.md)
[Steg 4 »](install-ata-step4.md)

## Steg 3. Hämta installationspaketet för ATA Gateway
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

## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)



<!--HONumber=Aug16_HO5-->


