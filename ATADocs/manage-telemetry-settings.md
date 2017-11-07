---
title: "Hantera telemetriinställningar för Advanced Threat Analytics | Microsoft Docs"
description: "Beskriver de data som samlas in av ATA och innehåller instruktioner för att inaktivera datainsamling."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/6/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a164179261dd5a50df973fab89be7ddce99f8c47
ms.sourcegitcommit: e2cb3af9c1dbb0b75946dc70cc439b19d654541c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/06/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="manage-telemetry-settings"></a>Hantera telemetriinställningar
ATA (Advanced Threat Analytics) samlar in anonymiserade telemetridata om ATA och överför data via en HTTPS-anslutning till Microsoft-servrar.  Dessa data används av Microsoft för att förbättra kommande versioner av ATA.

## <a name="data-collected"></a>Insamlade data
Insamlade anonymiserade data omfattar följande:

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
