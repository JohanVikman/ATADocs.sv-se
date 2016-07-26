---
title: "Hantera telemetriinställningar | Microsoft ATA"
description: "Beskriver de data som samlas in av ATA och innehåller instruktioner för att inaktivera datainsamling."
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 8c1c7a1b-a3de-4105-9fd0-08a061952172
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: b2b1ae963e8786b77c2fd124a612305be2c6b0bf


---

# Hantera telemetriinställningar
ATA (Advanced Threat Analytics) samlar in anonymiserade telemetridata om ATA och överför data via en HTTPS-anslutning till Microsoft-servrar.  Dessa data används av Microsoft för att förbättra kommande versioner av ATA.

## Insamlade data
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

### Inaktivera datainsamling
Utför följande steg om du vill sluta samla in och skicka telemetridata till Microsoft:

1.  Logga in på ATA-konsolen, klicka på de tre punkterna i verktygsfältet och välj **Om**.

2.  Avmarkera kryssrutan **Skicka användningsinformation till oss för att förbättra kundupplevelsen i framtiden**.

## Se även
- [Nyheter i version 1.6](/advanced-threat-analytics/understand-explore/whats-new-version-1.6)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


