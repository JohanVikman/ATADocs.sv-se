---
title: "Vad är nytt i ATA version 1.5 | Microsoft Advanced Threat Analytics"
description: "Visar en lista över vad som är nytt i ATA version 1.5 tillsammans med kända problem"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 5836792bcfadb2585d05d4a195979bd6003c84cf


---

# Nyheter i ATA version 1.5
Dessa versionsanmärkningar innehåller information om kända problem i denna version av Advanced Threat Analytics.

## Vad är nytt i ATA 1.5-uppdateringen?
Uppdateringen för ATA 1.5 ger förbättringar inom följande områden:

-   Snabbare identifiering

-   Förbättrad automatisk identifieringsalgoritm för NAT-enheter (Network address translation)

-   Förbättrad namnmatchningsprocess för icke-domänanslutna enheter

-   Stöd för migrering av data vid produktuppdateringar

-   Bättre gränssnittssvarstid för misstänkta aktiviteter när tusentals entiteter är inblandade

-   Förbättrad automatisk lösning för övervakningsvarningar

-   Ytterligare prestandaräknare för förbättrad övervakning och felsökning

## Kända problem
Följande kända problem finns i den här versionen.

### Den nya ATA Gateway-installationen misslyckas
När du har uppdaterat ATA-distributionen till ATA version 1.5 visas följande felmeddelande när du installerar en ny ATA Gateway: Microsoft Advanced Threat Analytics Gateway är inte installerat

![ATA GW-fel](media/ata-install-error.png)

<b>Lösning:</b> Skicka ett e-postmeddelande till <ataeval@microsoft.com> för att begära lösningssteg.
### distribution
Mappen som anges för "Datasökväg för databasen" och "Journalsökväg för databasen" måste vara tom (inga filer eller undermappar).
Distributionen kan inte gå vidare om mappen inte är tom.

### Installation från ZIP-fil
Tänk på att extrahera filerna från ZIP-filen till en lokal katalog och installera ATA Gateway därifrån. Installera inte ATA Gateway direkt från ZIP-filen eftersom installationen då misslyckas.

### Konfiguration
När konfigurationen för en ATA Gateway är klar och ATA Gateway startar för första gången visas etiketten "Ej synkroniserad" tills tjänsten har startats helt, vilket kan ta upp till 10 minuter första gången tjänsten startar.

### Programvara för nätverksavbildning
Den enda programvara för nätverksavbildning som går att installera på ATA Gateway är [Microsoft Network Monitor 3.4](http://www.microsoft.com/download/details.aspx?id=4865). Installera inte Microsoft Message Analyzer eller någon annan programvara för nätverksavbildning. Om annan programvara installeras kommer ATA Gateway att sluta fungera korrekt.

### KB på virtualiseringsvärd
Installera inte KB 3047154 på en virtualiseringsvärd. Det kan leda till att portspegling slutar fungera ordentligt.

## Se även

[Uppdatera ATA till version 1.5 – migreringsguide](ata-update-1.5-migration-guide.md)

[Uppdatera ATA till version 1.6 – migreringsguide](ata-update-1.6-migration-guide.md)

[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


