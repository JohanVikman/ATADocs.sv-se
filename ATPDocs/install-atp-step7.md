---
title: Installera Azure Advanced Threat Protection – steg 7 | Microsoft Docs
description: I det sista steget för att installera Azure ATP, konfigurerar du Honeytoken-användare.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/2/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7b3c128f6e2b524d778d68af7bcea65476cae2b7
ms.sourcegitcommit: 14c05a210ae92d35100c984ff8c6d171db7c3856
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 08/06/2018
ms.locfileid: "39568022"
---
*Gäller för: Azure Avancerat skydd*



# <a name="install-azure-atp---step-7"></a>Installera Azure ATP - steg 7

>[!div class="step-by-step"]
[« Steg 6](install-atp-step6-vpn.md)
[Steg 8 »](install-atp-step8-samr.md)

## <a name="step-7-configure-detection-exclusions-and-honeytoken-accounts"></a>Steg 7. Konfigurera identifiering av undantag och honeytoken-konton

Azure ATP aktiverar uteslutning av specifika IP-adresser eller användare från ett antal identifieringar. 

Till exempel kan ett **DNS-rekognoseringsundantag** vara en säkerhetsskanner som använder DNS som en skanningsmekanism. Undantaget hjälper Azure ATP ignorera dessa skannrar.  

Azure ATP möjliggör också konfiguration av honeytoken-konton som används som traps för skadliga aktörer – all verifiering som är associerade med de här honeytoken-konton (normalt vilande), utlöser en avisering.

Om du vill konfigurera, Följ dessa steg:

1.  Från Azure ATP-arbetsyteportalen, klicka på ikonen för inställningar och välj **Configuration**.

    ![Azure ATP-konfigurationsinställningar](media/atp-config-menu.png)

2.  Under **identifiering**, klickar du på **entitetstaggar**.

3. Under **Honeytoken-konton**, ange namnet på Honeytoken-kontot och klicka på den **+** inloggning. Fältet Honeytoken-konton är sökbart och visar automatiskt entiteter i nätverket. Klicka på **Spara**.

   ![Honeytoken](media/honeytoken-sensitive.png)

4. Klicka på **Undantag**. Ange ett användarkonto eller en IP-adress som ska undantas från identifiering, för varje typ av hot. 
5. Klicka på den *plus* inloggning. Fältet **Lägg till entitet** (användare eller dator) är sökbart och fylls automatiskt med entiteter i nätverket. Mer information finns i [exkludera entiteter från identifieringar](excluding-entities-from-detections.md) och [guide för misstänkt aktivitet](suspicious-activity-guide.md).

   ![Undantag](media/exclusions.png)

6.  Klicka på **Spara**.


Grattis, Azure Advanced Threat Protection har distribuerats!

På tidslinjen för attacker kan du visa identifierade misstänkta aktiviteter och söka efter användare eller datorer och visa deras profiler.

Azure ATP-sökning efter misstänkta aktiviteter startar omedelbart. Vissa identifieringar, till exempel onormalt Gruppändringar kräver en inlärningsperiod och är inte tillgängliga direkt efter Azure ATP-distributionen.



>[!div class="step-by-step"]
[« Steg 6](install-atp-step6-vpn.md)
[Steg 8 »](install-atp-step8-samr.md)

## <a name="see-also"></a>Se även
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Kolla in ATP-forumet!](https://aka.ms/azureatpcommunity)
