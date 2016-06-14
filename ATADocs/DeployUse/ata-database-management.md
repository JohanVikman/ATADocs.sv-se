---
# required metadata

title: ATA-databashantering | Microsoft Advanced Threat Analytics
description: Metoder som hjälper dig att flytta, säkerhetskopiera eller återställa ATA-databasen.
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA-databashantering
Om du behöver flytta, säkerhetskopiera eller återställa ATA-databasen kan du använda följande procedurer för att arbeta med MongoDB.

## Säkerhetskopiera ATA-databasen
Se [relevant MongoDB-dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## Återställa ATA-databasen
Se [relevant MongoDB-dokumentation](http://docs.mongodb.org/manual/administration/backup/).

## Flytta ATA-databasen till en annan enhet

1.  Stoppa tjänsten **Microsoft Advanced Threat Analytics Center**.

2.  Stoppa tjänsten **MongoDB**.

3.  Öppna Mongo-konfigurationsfilen som enligt standard finns på: C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg.

    Hitta parametern `storage: dbPath`

4.  Flytta mappen som anges i parametern `dbPath` till den nya platsen.

5.  Ändra parametern `dbPath` i Mongo-konfigurationsfilen till den nya mappsökvägen och spara och stäng filen.

    ![Bild för att ändra MongoDB-konfiguration](media/ATA-mongoDB-moveDB.png)

6.  Starta tjänsten **MongoDB**.

7.  Öppna en kommandotolk och kör Mongo-gränssnittet genom att köra `mongo.exe ATA` .

    Som standard finns mongo.exe på: C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin

8.  Kör följande kommando: `db.SystemProfiles.update( {_t: "CenterSystemProfile"} , {$set:{"Configuration.CenterDatabaseClientConfiguration.DataPath" : "<New DB Location>"}}) Instead of <New DB Location>` där &lt;Ny DB-plats&gt; är den nya mappsökvägen.

9.  Uppdatera HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath till den nya mappsökvägen.

9. Starta tjänsten **Microsoft Advanced Threat Analytics Center**.

## Se även
- [ATA-arkitektur](/advanced-threat-analytics/plan-design/ata-architecture)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO1-->


