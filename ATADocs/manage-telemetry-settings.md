---
title: Hantera Advanced Threat Analytics systemgenererade loggar | Microsoft Docs
description: Beskriver de data som samlas in av ATA och innehåller instruktioner för att inaktivera datainsamling.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 17e5778543b9f08d3157ed91cb0a7a73ea268c0a
ms.sourcegitcommit: 3539dd3f9ab7729e5326b904fc64985c808bc8ce
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 05/21/2018
---
*Gäller för: Advanced Threat Analytics version 1.9.*



# <a name="manage-system-generated-logs-note"></a>Hantera systemgenererade loggar > [!NOTE]
> Om du vill visa eller ta bort personliga data, läser du riktlinjerna för Microsofts i den [Microsoft Compliance Manager](https://servicetrust.microsoft.com/ComplianceManager) och i avsnittet [BNPR på webbplatsen Microsoft 365 Enterprise efterföljande] (https://docs.microsoft.com/en-us/microsoft-365/compliance/gdpr]. Om du letar efter allmän information om BNPR finns i [BNPR avsnitt av tjänsten förtroende portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).


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

- ATA-konsolens URL-adresser – URL-adresser när du använder ATA-konsolen, det vill säga vilka sidor i ATA-konsolen som besöks.


### <a name="disable-data-collection"></a>Inaktivera datainsamling
Utför följande steg om du vill sluta samla in och skicka telemetridata till Microsoft:

1.  Logga in på ATA-konsolen, klicka på de tre punkterna i verktygsfältet och välj **Om**.

2.  Avmarkera kryssrutan **Skicka användningsinformation till oss för att förbättra kundupplevelsen i framtiden**.

## <a name="see-also"></a>Se även
- [Felsöka ATA med händelseloggen](troubleshooting-ata-using-logs.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
