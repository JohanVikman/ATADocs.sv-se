---
title: Advanced Threat Analytics-databashantering | Microsoft Docs
description: Metoder som hjälper dig att flytta, säkerhetskopiera eller återställa ATA-databasen.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 20762e0d944adaa0c81de9f3ad1c32de445157fe
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 03/22/2018
ms.locfileid: "30009378"
---
*Gäller för: Advanced Threat Analytics version 1.9.*



# <a name="ata-database-management"></a>ATA-databashantering
Om du behöver flytta, säkerhetskopiera eller återställa ATA-databasen kan du använda följande procedurer för att arbeta med MongoDB.

## <a name="backing-up-the-ata-database"></a>Säkerhetskopiera ATA-databasen
Se [relevant MongoDB-dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## <a name="restoring-the-ata-database"></a>Återställa ATA-databasen
Se [relevant MongoDB-dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## <a name="moving-the-ata-database-to-another-drive"></a>Flytta ATA-databasen till en annan enhet

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

## <a name="see-also"></a>Se även
- [ATA-arkitektur](ata-architecture.md)
- [Krav för ATA](ata-prerequisites.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

