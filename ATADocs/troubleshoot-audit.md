---
title: Arbeta med ATA-granskningsloggar | Microsoft Docs
description: Den här artikeln beskriver hur du arbetar med ATA-granskningsloggar i Windows-händelseloggen.
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 5f4e7a51ca0a678b93d2b36bdafc885141dda1eb
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/07/2018
ms.locfileid: "44165957"
---
*Gäller för: Advanced Threat Analytics version 1.9*

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

* I granskningsloggen för konfigurationsändringar innehåller både den tidigare konfigurationen och den nya konfigurationen.


## <a name="see-also"></a>Se även
- [Arbeta med misstänkta aktiviteter](working-with-suspicious-activities.md)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
