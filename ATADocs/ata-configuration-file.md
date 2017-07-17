---
title: Exportera och importera Advanced Threat Analytics-konfiguration | Microsoft Docs
description: "Så här exporterar och importerar du ATA-konfigurationen."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/13/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: a04378838fab20c43df159ef3259530b8a599ed4
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 06/30/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# Exportera och importera ATA-konfigurationen
<a id="export-and-import-the-ata-configuration" class="xliff"></a>
Konfigurationen av ATA lagras i samlingen "SystemProfile" i databasen.
Den här samlingen säkerhetskopieras varje timme av ATA Center-tjänsten till filer som heter: "SystemProfile_*timestamp*.json". De senaste 10 versionerna lagras.
Den finns i en undermapp som heter "Backup". På standardplatsen för ATA-installation finns den här:  *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*timestamp*.json*. 

**Obs**! Vi rekommenderar att du säkerhetskopierar den här filen någonstans när du gör större ändringar av ATA.

Det går att återställa alla inställningar genom att köra följande kommando:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## Se även
<a id="see-also" class="xliff"></a>
- [ATA-arkitektur](ata-architecture.md)
- [Krav för ATA](ata-prerequisites.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

