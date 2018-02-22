---
title: Installera Azure Advanced Threat Protection - steg 7 | Microsoft Docs
description: "I det sista steget för att installera Azure ATP konfigurera honeytokenanvändaren."
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2017
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: bef13d0f4799a4483eda6604a8ed96befaa13508
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: MT
ms.contentlocale: sv-SE
ms.lasthandoff: 02/21/2018
---
*Gäller för: Azure Advanced Threat Protection*



# <a name="install-azure-atp---step-7"></a>Installera Azure ATP - steg 7

>[!div class="step-by-step"]
[« Steg 6](install-atp-step6-vpn.md)
[Steg 8 »](install-atp-step8-samr.md)

## <a name="step-7-configure-detection-exclusions-and-honeytoken-user"></a>Steg 7. Konfigurera undantag för identifiering och honeytokenanvändare

Azure ATP kan utesluta specifika IP-adresser eller användare från ett antal identifieringar. 

Till exempel kan ett **DNS-rekognoseringsundantag** vara en säkerhetsskanner som använder DNS som en skanningsmekanism. Undantag kan Azure ATP Ignorera sådana skannrar.  

Azure ATP gör det också möjligt för konfiguration av honeytokenanvändaren som används som en trap för skadliga aktörer - någon autentisering som är associerade med kontot (normalt vilande) utlöser en varning.

Följ dessa steg om du vill konfigurera detta:

1.  Från Azure ATP arbetsytan-portalen klickar du på ikonen för inställningar och väljer **Configuration**.

    ![Azure ATP-konfigurationsinställningar](media/atp-config-menu.png)

2.  Under **identifiering**, klickar du på **entitetstaggar**.

3. Under **Honeytoken konton** ange namnet på Honeytoken-kontot och klicka på den  **+**  tecken. Fältet Honeytoken konton är sökbar och visar automatiskt entiteter i nätverket. Klicka på **Spara**.

   ![Honeytoken](media/honeytoken-sensitive.png)

4. Klicka på **Undantag**. För varje typ av hot anger du ett användarkonto eller en IP-adress som ska uteslutas från identifieringen av dessa hot och klickar på *plustecknet*. Fältet **Lägg till entitet** (användare eller dator) är sökbart och fylls automatiskt med entiteter i nätverket. Mer information finns i [exkludera entiteter från identifieringar](excluding-entities-from-detections.md) och [misstänkt aktivitet guiden](suspicious-activity-guide.md).

   ![Undantag](media/exclusions.png)

5.  Klicka på **Spara**.


Grattis, Azure Advanced Threat Protection har distribuerats!

På tidslinjen för attacker kan du visa identifierade misstänkta aktiviteter och söka efter användare eller datorer och visa deras profiler.

Azure ATP startar sökning efter misstänkta aktiviteter omedelbart. Vissa identifieringar som onormal grupp ändringar kräver en utbildning och är inte tillgängliga direkt efter distributionen av Azure ATP.



>[!div class="step-by-step"]
[« Steg 6](install-atp-step6-vpn.md)
[Steg 8 »](install-atp-step8-samr.md)

## <a name="see-also"></a>Se även
- [Azure ATP-storleksverktyget](http://aka.ms/aatpsizingtool)
- [Konfigurera händelseinsamling](configure-event-collection.md)
- [Krav för Azure ATP](atp-prerequisites.md)
- [Ta en titt i ATP-forumet!](https://aka.ms/azureatpcommunity)
