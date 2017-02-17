---
title: Exportera och importera Advanced Threat Analytics-konfiguration | Microsoft Docs
description: "Så här exporterar och importerar du ATA-konfigurationen."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 5ea29a5b64fd1f786200d3bbb62cd3964f8802e2


---

*Gäller för: Advanced Threat Analytics version 1.7*



# <a name="export-and-import-the-ata-configuration"></a>Exportera och importera ATA-konfigurationen
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




<!--HONumber=Feb17_HO1-->


