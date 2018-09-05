---
title: Exportera och importera Advanced Threat Analytics-konfiguration | Microsoft Docs
description: Så här exporterar och importerar du ATA-konfigurationen.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/04/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: f8847d8ca3671f765a1d101121eefad62073f60f
ms.sourcegitcommit: 6f1406f28c4c2af6a36bc691ebaf4e819adc6b4b
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43675159"
---
*Gäller för: Advanced Threat Analytics version 1.9*



# <a name="export-and-import-the-ata-configuration"></a>Exportera och importera ATA-konfigurationen
Konfigurationen av ATA lagras i samlingen "SystemProfile" i databasen.
Den här samlingen säkerhetskopieras var 4 timme av ATA Center-tjänsten till filer som heter: **SystemProfile_*tidsstämpel*.json**. 300 de senaste versionerna lagras.
Den här filen finns i undermappen **Backup**. På standardplatsen för ATA-installation finns den här:  *C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_* timestamp *.json*. 

**Obs**! Vi rekommenderar att du säkerhetskopierar den här filen någonstans när du gör större ändringar av ATA.

Det går att återställa alla inställningar genom att köra följande kommando:

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>Se även
- [ATA-arkitektur](ata-architecture.md)
- [Krav för ATA](ata-prerequisites.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

