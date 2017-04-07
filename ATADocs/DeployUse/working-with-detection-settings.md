---
title: "Ställ in identifieringsinställningar i Advanced Threat Analytics | Microsoft Docs"
description: "Beskriver hur du konfigurerar en lista över IP-adresser och undernät som har ovanliga omständigheter och som bör hanteras annorlunda än andra entiteter i nätverket"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 831bafd08e0eea821fda94bd4f519d92ffec3397
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
*Gäller för: Advanced Threat Analytics version 1.7*



# <a name="working-with-ata-detection-settings"></a>Arbeta med identifieringsinställningar i ATA
På konfigurationssidan **Identifiering** kan du ange en lista över IP-adresser och undernät som har ovanliga omständigheter och bör hanteras lite annorlunda än andra entiteter i nätverket.

## <a name="setting-up-detection"></a>Konfigurera identifiering
I avsnittet **Identifiering** kan du definiera följande objekt:

-   **Honeytokenkonto-SID** – det här är ett användarkonto som inte bör ha några nätverksaktiviteter. Det här kontot konfigureras som ATA-honeytokenanvändaren. Om någon försöker använda det här användarkontot skapar ATA en misstänkt aktivitet. Det är en indikation på skadlig aktivitet. Om du vill konfigurera honeytokenanvändaren behöver du användarkontots SID, inte användarnamnet.

>[!NOTE]
> Du kan hitta SID för användaren på fliken *Kontoinformation* i användarens profil i ATA-konsolen.


![Honeytoken för ATA-identifieringsinställningar](media/ata-detection-settings-honeytoken-1.7.png)


**Identifieringsundantag** - Du kan undanta IP-adresser från följande identifieringar. Om du anger en IP-adress i en av de här listorna undantar ATA den IP-adressen från den här specifika typen av identifierad aktivitet.

-   Undantag för DNS Reconnaissance-IP-adresser

-   Undantag för Pass-the-Ticket-IP-adresser

![Undantag för ATA-identifieringsinställningar](media/ata-detection-settings-exclusions-1.7.png)


## <a name="see-also"></a>Se även
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ändra ATA-konfiguration](modifying-ata-configuration.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
