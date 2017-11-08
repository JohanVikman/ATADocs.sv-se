---
title: Arbeta med ATA-granskningsloggar | Microsoft Docs
description: "Den här artikeln beskriver hur du arbetar med ATA-granskningsloggar i Windows-händelseloggen."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 287bb370f216c2f921eb954dfd4a34ceb8f095c7
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 11/07/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*

# <a name="working-with-ata-audit-logs"></a>Arbeta med ATA-granskningsloggar

ATA-granskningsloggarna sparas i Windows-händelseloggarna under **Program och tjänster** och sedan **Microsoft ATA** både på ATA Center- och ATA Gateway-datorerna.

ATA Center-granskningsloggen innehåller:
-   Information om misstänkt aktivitet
-   Övervakningsaviseringar (hälsotillståndssidan)
-   Inloggningar till ATA-konsolen
-   Alla konfigurationsändringar*

ATA Gateway-granskningsloggen innehåller:
-   Ändringar av gatewaykonfigurationen * 

(Alla ATA Gateway-konfigurationsändringar konfigureras på ATA Center men granskas fortfarande på själva gatewaydatorn.)

* Configuration ändra granskningsloggen innehåller både den tidigare konfigurationen och den nya konfigurationen.


## <a name="see-also"></a>Se även
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
