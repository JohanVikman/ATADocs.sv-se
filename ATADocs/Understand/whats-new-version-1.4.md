---
# required metadata

title: Nyheter i ATA version 1.4 | Microsoft Advanced Threat Analytics
description: Visar en lista över nyheter i ATA version 1.4 tillsammans med kända problem
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: cbea47f9-34c1-42b6-ae9e-6a472b49e1a5

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# Nyheter i ATA version 1.4
Dessa versionsanmärkningar innehåller information om kända problem i version 1.4 av Advanced Threat Analytics.

## Nyheter i den här versionen

-   Stöd för WEF (Windows Event Forwarding) för att skicka händelser direkt från domänkontrollanterna till ATA-gatewayen.

-   Förbättringar av Pass-The-Hash-identifiering på företagsresurser genom att kombinera djup paketinspektion (DPI) och Windows-händelseloggar.

-   Förbättringar av stödet för icke-domänanslutna enheter och icke-Windows-enheter för identifiering och synlighet.

-   Prestandaförbättringar för stöd för mer trafik per ATA-gateway.

-   Prestandaförbättringar för stöd för fler ATA-gatewayer per ATA Center.

-   En ny automatisk namnmatchningsprocess har lagts till som matchar datornamn och IP-adresser – den här unika funktionen sparar värdefull tid i undersökningsprocessen och ger starka bevis för säkerhetsanalytiker

-   Förbättrad möjlighet att samla in indata från användare för att automatiskt finjustera identifieringsprocessen.

-   Automatisk identifiering för NAT-enheter.

-   Automatisk redundans när domänkontrollanter inte kan nås.

-   Övervakning av systemhälsa och aviseringar visar nu det övergripande hälsotillståndet för distributionen och specifika problem som är relaterade till konfiguration och anslutning.

-   Inblick i webbplatser och platser där entiteter är i drift.

-   Stöd för flera domäner.

-   Stöd för enkla domännamn utan toppdomän (SLD).

-   Stöd för att ändra IP-adressen och certifikatet för ATA-gatewayerna och ATA Center.

-   Telemetri för att förbättra kundupplevelsen.

## Kända problem
Följande kända problem finns i den här versionen.

### Programvara för nätverksavbildning
Den enda programvara för nätverksavbildning som går att installera på ATA Gateway är [Microsoft Network Monitor 3.4](http://www.microsoft.com/en-us/download/details.aspx?id=4865). Installera inte Microsoft Message Analyzer eller någon annan programvara för nätverksavbildning. Om annan programvara installeras kommer ATA Gateway att sluta fungera korrekt.

### Installation från ZIP-fil
Tänk på att extrahera filerna från ZIP-filen till en lokal katalog och installera ATA Gateway därifrån. Installera inte ATA Gateway direkt från ZIP-filen eftersom installationen då misslyckas.

### Avinstallera tidigare versioner av ATA
Om du har installerat en tidigare version av ATA, en offentlig förhandsversion eller en privat förhandsversion måste du avinstallera ATA Center och ATA-gatewayerna innan du installerar den här versionen av ATA.

Du måste även ta bort databasfilerna och loggfilerna. Databaserna från tidigare versioner av ATA är inte kompatibla med GA-versionen av ATA.

Om ATA-installationen öppnas i stället för avinstallationen när du försöker avinstallera ATA Center eller ATA Gateway behöver du lägga till följande registernyckel och sedan avinstallera ATA igen.

**ATA Center**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center

-   Lägg till ett nytt strängvärde med namnet `InstallationPath` och värdet `C:\Program Files\Microsoft Advanced Threat Analytics\Center`. Det är standardinstallationsmappen. Om du har ändrat installationsmappen anger du sökvägen där ATA har installerats.

    ![Registereditorn för installationssökvägen för ATA Center](media/ATA-uninstall-center-bug.jpg)

**ATA Gateway**

-   HKLM\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Gateway

-   Lägg till ett nytt strängvärde med namnet `InstallationPath` och värdet `C:\Program Files\Microsoft Advanced Threat Analytics\Gateway`. Det är standardinstallationsmappen.  Om du har ändrat installationsmappen anger du sökvägen där ATA har installerats.

    ![Registereditorn för installationssökvägen för ATA Gateway](media/ATA-GW-uninstall-bug.jpg)

Ta bort installationsmappen på både ATA Center och ATA Gateway efter avinstallationen.  Om du har installerat databasen i en separat mapp tar du bort databasmappen på ATA Center.

### Hälsoavisering – frånkopplad ATA-gateway
Om du har fler än en ATA-gateway och har aviseringar om frånkopplad ATA-gateway fungerar automatisk matchning bara på en av dem. Resten lämnas med öppen status. Du måste manuellt bekräfta att ATA-gatewayen är tillgänglig och att tjänsten körs och lösa aviseringen manuellt.

### KB på virtualiseringsvärd
Installera inte KB 3047154 på en virtualiseringsvärd. Det kan leda till att portspegling slutar fungera ordentligt.

## Se även

[Uppdatera ATA till version 1.6 – migreringsguide](ata-update-1.6-migration-guide.md)

[Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)

<!--HONumber=May16_HO3-->


