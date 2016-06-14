---
# required metadata

title: Installera ATA – Steg 3 | Microsoft Advanced Threat Analytics
description: Steg tre av ATA-installationen hjälper dig att hämta installationspaketet för ATA Gateway.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 7fb024e6-297a-4ad9-b962-481bb75a0ba3

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Installera ATA – Steg 3

>[!div class="step-by-step"]
[« Steg 2](install-ata-step2.md)
[Steg 4 »](install-ata-step4.md)

## Steg 3. Hämta installationspaketet för ATA Gateway
När du har konfigurerat anslutningsinställningarna för domänen kan du hämta ATA Gateway-installationspaketet. ATA Gateway kan installeras på dedikerad server eller en domänkontrollant. Om du installerar den på en domänkontrollant kommer den att installeras som en ATA Lightweight Gateway. Mer information om ATA Lightweight Gateway finns i [ATA-arkitektur](/advanced-threat-analytics/plan-design/ata-architecture). 

Hämta ATA Gateway-paketet:

1.  Från ATA-konsolen klickar du på inställningsikonen och väljer **Konfiguration**.

    ![Konfigurationsinställningar för ATA Gateway](media/ATA-config-icon.JPG)

2.  På fliken **ATA Gateways** klickar du på **Hämta installationsprogram för ATA Gateway**.

3.  Spara paketet lokalt.
4.  Kopiera paketet till den dedikerade servern eller domänkontrollanten där du installerar ATA Gateway. Du kan även öppna ATA-konsolen från den dedikerade servern eller domänkontrollanten och hoppa över detta steg.

ZIP-filen innehåller följande:

-   Installationsprogram för ATA Gateway

-   Filen med konfigurationsinställningar som innehåller informationen som krävs för att ansluta till ATA Center


>[!div class="step-by-step"]
[« Steg 2](install-ata-step2.md)
[Steg 4 »](install-ata-step4.md)

## Se även

- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)


<!--HONumber=May16_HO1-->


