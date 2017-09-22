---
title: Installera Advanced Threat Analytics - steg 8 | Microsoft Docs
description: "I det sista ATA-installationssteget konfigurerar du Honeytoken-användaren."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 09/19/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3a8ccb1412bbd8e2013c84d36f4142301159c46c
ms.sourcegitcommit: 34c3d6f56f175994b672842c7576040956ceea69
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 09/19/2017
---
*Gäller för: Advanced Threat Analytics version 1.8*



# <a name="install-ata---step-8"></a>Installera ATA – steg 8

>[!div class="step-by-step"]
[«Steg 7](vpn-integration-install-step.md)

## <a name="step-8-configure-ip-address-exclusions-and-honeytoken-user"></a>Steg 8. Konfigurera undantag för IP-adress och Honeytoken-användare
Du kan utesluta specifika IP-adresser eller användare från ett antal identifieringar i ATA. 

Till exempel kan ett **DNS-rekognoseringsundantag** vara en säkerhetsskanner som använder DNS som en skanningsmekanism. Undantaget hjälper ATA att ignorera dessa skannrar. Ett exempel på ett *Pass-the-Ticket*-undantag är en NAT-enhet.    

ATA möjliggör också konfiguration av en Honeytoken-användare som används som en fälla för skadliga aktörer – all verifiering som är associerade med kontot (normalt vilande) ska utlösa en avisering.

Följ de här stegen när du ska konfigurera ovan nämnda:

1.  I ATA-konsolen klickar du på inställningsikonen och väljer **Konfiguration**.

    ![Konfigurationsinställningar för ATA](media/ATA-config-icon.png)

2.  Klicka på **Allmänt** under **Identifiering**.

2. Ange namnet på Honeytoken-kontot under **Honeytoken-konton**. Fältet Honeytoken-konton är sökbart och visar automatiskt entiteter i ditt nätverk.

   ![Honeytoken](media/honeytoken.png)

3. Klicka på **Undantag**. För varje typ av hot anger du ett användarkonto eller en IP-adress som ska uteslutas från identifieringen av dessa hot och klickar på *plustecknet*. Fältet **Lägg till entitet** (användare eller dator) är sökbart och fylls automatiskt med entiteter i nätverket. Mer information finns i [Exkludera entiteter från att identifieras](excluding-entities-from-detections.md)

   ![Undantag](media/exclusions.png)

4.  Klicka på **Spara**.


Gratulerar, Microsoft Advanced Threat Analytics har distribuerats!

På tidslinjen för attacker kan du visa identifierade misstänkta aktiviteter och söka efter användare eller datorer och visa deras profiler.

ATA startar sökning efter misstänkta aktiviteter omedelbart. En del aktiviteter, t.ex. vissa av aktiviteterna för misstänkt beteende, är inte tillgängliga förrän ATA har fått tid att skapa beteendeprofiler (minst tre veckor).

I [ATA-boken med simulerade attacker](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook) kan du kontrollera att ATA är igång ordentligt och identifierar överträdelser i nätverket.


>[!div class="step-by-step"]
[«Steg 7](vpn-integration-install-step.md)



## <a name="related-videos"></a>Relaterade videor
- [Välja rätt ATA Gateway-typ](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>Se även
- [ATA POC Distributionsguide](http://aka.ms/atapoc)
- [ATA-storleksverktyget](http://aka.ms/atasizingtool)
- [Ta en titt i ATA-forumet!](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för ATA](ata-prerequisites.md)

