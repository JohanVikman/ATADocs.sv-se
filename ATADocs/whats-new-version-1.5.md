---
title: Nyheter i Advanced Threat Analytics version 1.5 | Microsoft Docs
description: Visar en lista över vad som är nytt i ATA version 1.5 tillsammans med kända problem
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a00a555c0dc4590043f93abcd650f6e38d719e6c
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2017
ms.locfileid: "24018277"
---
# <a name="whats-new-in-ata-version-15"></a>Nyheter i ATA version 1.5
Dessa versionsanmärkningar innehåller information om kända problem i denna version av Advanced Threat Analytics.

## <a name="whats-new-in-the-ata-15-update"></a>Vad är nytt i ATA 1.5-uppdateringen?
Uppdateringen för ATA 1.5 ger förbättringar inom följande områden:

-   Snabbare identifiering

-   Förbättrad automatisk identifieringsalgoritm för NAT-enheter (Network address translation)

-   Förbättrad namnmatchningsprocess för icke-domänanslutna enheter

-   Stöd för migrering av data vid produktuppdateringar

-   Bättre gränssnittssvarstid för misstänkta aktiviteter när tusentals entiteter är inblandade

-   Förbättrad automatisk lösning för övervakningsvarningar

-   Ytterligare prestandaräknare för förbättrad övervakning och felsökning

## <a name="known-issues"></a>Kända problem
Följande kända problem finns i den här versionen.

### <a name="new-ata-gateway-installation-fails"></a>Den nya ATA Gateway-installationen misslyckas
När du har uppdaterat ATA-distributionen till ATA version 1.5 visas följande felmeddelande när du installerar en ny ATA Gateway: Microsoft Advanced Threat Analytics Gateway är inte installerat

![ATA GW-fel](media/ata-install-error.png)

<b>Lösning:</b> Skicka ett e-postmeddelande till <ataeval@microsoft.com> för att begära lösningssteg.
### <a name="deployment"></a>distribution
Mappen som anges för "Datasökväg för databasen" och "Journalsökväg för databasen" måste vara tom (inga filer eller undermappar).
Distributionen inte gå vidare om det inte är tom.

### <a name="installation-from-zip-file"></a>Installation från ZIP-fil
Tänk på att extrahera filerna från ZIP-filen till en lokal katalog och installera ATA Gateway därifrån. Installera inte ATA Gateway direkt från zip-filen eller misslyckas installationen.

### <a name="configuration"></a>Konfiguration
När konfigurationen för en ATA Gateway är klar och ATA Gateway startar för första gången visas etiketten "Ej synkroniserad" tills tjänsten har startats helt, vilket kan ta upp till 10 minuter första gången tjänsten startar.

### <a name="network-capture-software"></a>Programvara för nätverksavbildning
Den enda programvara för nätverksavbildning som går att installera på ATA Gateway är [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865). Installera inte Microsoft Message Analyzer eller någon annan programvara för nätverksavbildning. Om annan programvara installeras kommer ATA Gateway att sluta fungera korrekt.

### <a name="kb-on-virtualization-host"></a>KB på virtualiseringsvärd
Installera inte KB 3047154 på en virtualiseringsvärd. Det kan leda till att portspegling slutar fungera ordentligt.

## <a name="see-also"></a>Se även

[Uppdatera ATA till version 1.5 – migreringsguide](ata-update-1.5-migration-guide.md)

[Uppdatera ATA till version 1.6 – migreringsguide](ata-update-1.6-migration-guide.md)

[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
