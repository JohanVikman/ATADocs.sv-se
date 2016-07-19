---
title: "Arbeta med identifieringsinställningar i ATA | Microsoft Advanced Threat Analytics"
description: "Beskriver hur du konfigurerar en lista över IP-adresser och undernät som har ovanliga omständigheter och som bör hanteras annorlunda än andra entiteter i nätverket"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 8d1dedaf86031e8585cca23241aead58f7f3db4e
ms.openlocfilehash: 3840a5f7abdd496ad245a3f1c2589ad1855fddb5


---

# Arbeta med identifieringsinställningar i ATA
På konfigurationssidan **Identifiering** kan du ange en lista över IP-adresser och undernät som har ovanliga omständigheter och bör hanteras lite annorlunda än andra entiteter i nätverket.

## Konfigurera identifiering
På sidan **Identifiering** kan du definiera följande objekt:

-   **Undernät med kortsiktiga lån** – om organisationen har undernät där IP-adresserna är mycket kortsiktiga, till exempel undernät med IP-adresser för VPN eller Wi-Fi-undernät, är det viktigt att ange IP-adresserna och undernäten i ATA så att ATA lagrar associationen mellan en dator och en IP-adress från dessa intervall under kortare tid än för andra IP-adresser.

-   **Honeytokenkonto-SID** – det här är ett användarkonto som inte bör ha några nätverksaktiviteter. Det här kontot konfigureras som ATA-honeytokenanvändaren. Om någon försöker använda det här användarkontot skapar ATA en misstänkt aktivitet. Det är en indikation på skadlig aktivitet. Om du vill konfigurera honeytokenanvändaren behöver du användarkontots SID, inte användarnamnet.

Du kan undanta IP-adresser från följande identifieringar. Om du anger en IP-adress i en av de här listorna undantar ATA den IP-adressen från den här specifika typen av identifierad aktivitet.

-   Undantag för DNS Reconnaissance-IP-adresser

-   Undantag för Pass-the-Ticket-IP-adresser

## Se även
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ändra ATA-konfiguration](modifying-ata-configuration.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jun16_HO4-->


