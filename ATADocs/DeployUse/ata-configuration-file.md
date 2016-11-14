---
title: ATA-konfigurationsfil | Microsoft ATA
description: "Säkerhetskopiera ATA-konfiguration."
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
ms.openlocfilehash: 542bdf983e26fa98c036de55860b482d0b1d734d


---

*Gäller för: Advanced Threat Analytics version 1.7*



# <a name="ata-configuration-file"></a>ATA-konfigurationsfil
Konfigurationen av ATA lagras i samlingen "SystemProfile" i databasen.
Den här samlingen säkerhetskopieras varje timme av ATA Center-tjänsten till filer som heter: "SystemProfile_*timestamp*.json". De senaste 10 versionerna lagras.
Den finns i en undermapp som heter "Backup". På standardplatsen för ATA-installation finns den här:  *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*timestamp*.json*. 

**Obs**! Vi rekommenderar att du säkerhetskopierar den här filen någonstans när du gör större ändringar av ATA.

Det går att återställa alla inställningar genom att köra följande kommando:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Se även
- [ATA-arkitektur](/advanced-threat-analytics/plan-design/ata-architecture)
- [Krav för ATA](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Oct16_HO5-->


