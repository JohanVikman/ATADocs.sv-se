---
title: Advanced Threat Analytics-databashantering | Microsoft Docs
description: "Metoder som hjälper dig att flytta, säkerhetskopiera eller återställa ATA-databasen."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4fe667574ea011c032bacd8f5bce4b07c2c46602
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/30/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# ATA-databashantering
<a id="ata-database-management" class="xliff"></a>
Om du behöver flytta, säkerhetskopiera eller återställa ATA-databasen kan du använda följande procedurer för att arbeta med MongoDB.

## Säkerhetskopiera ATA-databasen
<a id="backing-up-the-ata-database" class="xliff"></a>
Se [relevant MongoDB-dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## Återställa ATA-databasen
<a id="restoring-the-ata-database" class="xliff"></a>
Se [relevant MongoDB-dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## Flytta ATA-databasen till en annan enhet
<a id="moving-the-ata-database-to-another-drive" class="xliff"></a>

1.  Stoppa tjänsten **Microsoft Advanced Threat Analytics Center**.
> [!Important] 
> Kontrollera att ATA Center-tjänsten stoppats innan du går vidare till nästa steg.

2.  Stoppa tjänsten **MongoDB**.

3.  Öppna Mongo-konfigurationsfilen som enligt standard finns på: C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Hitta parametern `storage: dbPath`

4.  Flytta mappen som anges i parametern `dbPath` till den nya platsen.

5.  Ändra parametern `dbPath` i Mongo-konfigurationsfilen till den nya mappsökvägen och spara och stäng filen.

    ![Bild för att ändra MongoDB-konfiguration](media/ATA-mongoDB-moveDB.png)

6.  Starta tjänsten **MongoDB**.

7. Starta tjänsten **Microsoft Advanced Threat Analytics Center**.

## Se även
<a id="see-also" class="xliff"></a>
- [ATA-arkitektur](ata-architecture.md)
- [Krav för ATA](ata-prerequisites.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

