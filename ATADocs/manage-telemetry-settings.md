---
title: Hantera systemgenererade loggar i Advanced Threat Analytics | Microsoft Docs
description: Beskriver de data som samlas in av ATA och innehåller instruktioner för att inaktivera datainsamling.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/26/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1216d70f75376f295e9b6164babdaf24241195b4
ms.sourcegitcommit: 7d025a2518ce63f38ce609dc21d8c3bacdd6a8e7
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/26/2018
ms.locfileid: "36948922"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="manage-system-generated-logs-note"></a>Hantera systemgenererade loggar > [!NOTE]

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

Advanced Threat Analytics (ATA) samlar in anonymiserade loggdata för systemgenererade om ATA och överför data via en HTTPS-anslutning till Microsoft-servrar.  Dessa data används av Microsoft för att förbättra kommande versioner av ATA.

## <a name="data-collected"></a>Insamlade data
Insamlade anonymiserade data omfattar följande parametrar:

-   Prestandaräknare från både ATA Center och ATA Gateway

-   Produkt-ID från licensierade exemplar av ATA

-   Distributionsdatum för ATA Center

-   Antal distribuerade ATA-gatewayer

-   Följande anonymiserade Active Directory-information:

    -   Domän-ID för domänen vars namn är den första domänen när de sorteras alfabetiskt

    -   Antal domänkontrollanter

    -   Antal domänkontrollanter som övervakas av ATA via portspegling

    -   Antal webbplatser

    -   Antal datorer

    -   Antal grupper

    -   Antal användare

-   Misstänkta aktiviteter – följande anonymiserade data samlas in för varje misstänkt aktivitet:

    (Datornamn, användarnamn och IP-adresser samlas **inte** in)

    -   Typ av misstänkt aktivitet

    -   ID för misstänkt aktivitet

    -   Status

    -   Start- och sluttid

    -   Indata som angetts

- Problem med hälsotillstånd – följande avidentifierade data samlas in för varje hälsotillståndsproblem:

    (Datornamn, användarnamn och IP-adresser samlas inte in)

    -   Typ av hälsotillståndsproblem

    -   ID för hälsotillståndsproblem

    -   Status

    -   Start- och sluttid

- ATA-konsolens URL-adresser - webbadresser vid användning av ATA-konsolen, d.v.s. vilka sidor i ATA-konsolen som besöks.


### <a name="disable-data-collection"></a>Inaktivera datainsamling
Utför följande steg om du vill sluta samla in och skicka telemetridata till Microsoft:

1.  Logga in på ATA-konsolen, klicka på de tre punkterna i verktygsfältet och välj **Om**.

2.  Avmarkera kryssrutan **Skicka användningsinformation till oss för att förbättra kundupplevelsen i framtiden**.

## <a name="see-also"></a>Se även
- [Felsöka ATA med händelseloggen](troubleshooting-ata-using-logs.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
