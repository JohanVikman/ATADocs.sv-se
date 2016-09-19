---
title: ATA-databashantering | Microsoft ATA
description: "Metoder som hjälper dig att flytta, säkerhetskopiera eller återställa ATA-databasen."
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5cd030f3b952d08c6617a6cda121c344a9c36f51
ms.openlocfilehash: b4e68e9e8dbd94075a34a8e3e8f42d4f534caf50


---

*Gäller för: Advanced Threat Analytics version 1.7*



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

7. Starta tjänsten **Microsoft Advanced Threat Analytics Center**.

## ATA-konfigurationsfil
Konfigurationen av ATA lagras i samlingen "SystemProfile" i databasen.
Den här samlingen säkerhetskopieras varje timme av ATA Center-tjänsten till filer som heter: "SystemProfile_*timestamp*.json". De senaste 10 versionerna lagras.
Den finns i en undermapp som heter "Backup". På standardplatsen för ATA-installation finns den här:  *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*timestamp*.json*. 

**Obs**! Vi rekommenderar att du säkerhetskopierar den här filen någonstans när du gör större ändringar av ATA.

Det går att återställa alla inställningar genom att köra följande kommando:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## Se även
- [ATA-arkitektur](/advanced-threat-analytics/plan-design/ata-architecture)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Aug16_HO5-->


