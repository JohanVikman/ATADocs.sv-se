---
title: ATA-databashantering | Microsoft ATA
description: "Metoder som hjälper dig att flytta, säkerhetskopiera eller återställa ATA-databasen."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 10/31/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f334f9c8440e4bb0202579de220f6530d0aabad8
ms.openlocfilehash: e295e0a0a8b5adbd40ddeb7e389ff82c7482c6d9


---

*Gäller för: Advanced Threat Analytics version 1.7*



# <a name="ata-database-management"></a>ATA-databashantering
Om du behöver flytta, säkerhetskopiera eller återställa ATA-databasen kan du använda följande procedurer för att arbeta med MongoDB.

## <a name="backing-up-the-ata-database"></a>Säkerhetskopiera ATA-databasen
Se [relevant MongoDB-dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## <a name="restoring-the-ata-database"></a>Återställa ATA-databasen
Se [relevant MongoDB-dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## <a name="moving-the-ata-database-to-another-drive"></a>Flytta ATA-databasen till en annan enhet

1.  Stoppa tjänsten **Microsoft Advanced Threat Analytics Center**.

2.  Stoppa tjänsten **MongoDB**.

3.  Öppna Mongo-konfigurationsfilen som enligt standard finns på: C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Hitta parametern `storage: dbPath`

4.  Flytta mappen som anges i parametern `dbPath` till den nya platsen.

5.  Ändra parametern `dbPath` i Mongo-konfigurationsfilen till den nya mappsökvägen och spara och stäng filen.

    ![Bild för att ändra MongoDB-konfiguration](media/ATA-mongoDB-moveDB.png)

6.  Starta tjänsten **MongoDB**.

7. Starta tjänsten **Microsoft Advanced Threat Analytics Center**.

## <a name="see-also"></a>Se även
- [ATA-arkitektur](/advanced-threat-analytics/plan-design/ata-architecture)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Oct16_HO5-->


