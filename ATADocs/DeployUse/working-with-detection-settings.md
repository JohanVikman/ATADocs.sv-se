---
title: "Arbeta med identifieringsinställningar i ATA | Microsoft ATA"
description: "Beskriver hur du konfigurerar en lista över IP-adresser och undernät som har ovanliga omständigheter och som bör hanteras annorlunda än andra entiteter i nätverket"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 28b6211599395317eb6336c37fd3461b8f5635f6
ms.openlocfilehash: 09248cdd5f8a66a164a5cd275f2765107f5c706d


---

*Gäller för: Advanced Threat Analytics version 1.7*



# Arbeta med identifieringsinställningar i ATA
På konfigurationssidan **Identifiering** kan du ange en lista över IP-adresser och undernät som har ovanliga omständigheter och bör hanteras lite annorlunda än andra entiteter i nätverket.

## Konfigurera identifiering
I avsnittet **Identifiering** kan du definiera följande objekt:

-   **Honeytokenkonto-SID** – det här är ett användarkonto som inte bör ha några nätverksaktiviteter. Det här kontot konfigureras som ATA-honeytokenanvändaren. Om någon försöker använda det här användarkontot skapar ATA en misstänkt aktivitet. Det är en indikation på skadlig aktivitet. Om du vill konfigurera honeytokenanvändaren behöver du användarkontots SID, inte användarnamnet.

>[!NOTE]
> Du kan hitta SID för användaren på fliken *Kontoinformation* i användarens profil i ATA-konsolen.


![Honeytoken för ATA-identifieringsinställningar](media/ata-detection-settings-honeytoken-1.7.png)


**Identifieringsundantag** - Du kan undanta IP-adresser från följande identifieringar. Om du anger en IP-adress i en av de här listorna undantar ATA den IP-adressen från den här specifika typen av identifierad aktivitet.

-   Undantag för DNS Reconnaissance-IP-adresser

-   Undantag för Pass-the-Ticket-IP-adresser

![Undantag för ATA-identifieringsinställningar](media/ata-detection-settings-exclusions-1.7.png)


## Se även
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ändra ATA-konfiguration](modifying-ata-configuration.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Aug16_HO5-->


